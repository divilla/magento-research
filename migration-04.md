# Splitting Magento modules into frontend, backend, and APIs

Magento modules can contain separate frontend, backend, admin, API, and integration code, but they are normally packaged and deployed as one PHP module inside the same Magento application.

They are logically separated, not necessarily independently deployable services.

## Typical module decomposition

A module can be viewed as four parts:

```text
Magento module
├── Domain/backend logic
├── Storefront presentation
├── Admin presentation
└── API and integration surface
```

### Backend/domain logic

This contains the actual business behavior:

```text
Model/
Api/
Service/
Plugin/
Observer/
Cron/
Console/
Setup/
etc/di.xml
etc/events.xml
etc/crontab.xml
etc/db_schema.xml
```

Examples include:

- Price calculation
- Order validation
- ERP synchronization
- Inventory changes
- Scheduled processing
- Database persistence

### Storefront frontend

Storefront-specific files commonly appear under:

```text
view/frontend/
├── layout/
├── templates/
├── web/js/
├── web/css/
└── web/template/

Controller/
etc/frontend/
```

This part renders pages and modifies browser behavior.

### Admin frontend

Admin functionality normally appears under:

```text
view/adminhtml/
├── layout/
├── templates/
├── ui_component/
└── web/

Controller/Adminhtml/
Ui/
Block/Adminhtml/
etc/adminhtml/
```

It can provide:

- Configuration screens
- Data grids
- Forms
- Administrative actions
- Permissions

### APIs

A module may expose or consume several API types:

```text
etc/webapi.xml          REST/SOAP exposure
etc/webapi_async.xml    asynchronous APIs
etc/schema.graphqls     GraphQL schema
Api/                    PHP service contracts
Model/Resolver/         GraphQL resolvers
etc/queue*.xml          message queues
```

The module can also call external APIs using ordinary PHP HTTP clients.

## Areas are explicit

Magento supports scoped configuration areas:

```text
etc/
etc/frontend/
etc/adminhtml/
etc/graphql/
etc/webapi_rest/
etc/webapi_soap/
etc/crontab/
```

This is useful for analysis because the path often reveals where a customization operates. For example:

```text
etc/frontend/events.xml
```

indicates a storefront-area observer, while:

```text
etc/webapi_rest/di.xml
```

changes dependency injection specifically during REST requests.

However, a globally declared plugin in `etc/di.xml` may execute in multiple areas. The directory structure alone does not guarantee isolation.

## Can an existing module be separated?

Usually yes, conceptually. Consider a module that adds delivery-date selection:

```text
Frontend:
- Calendar widget
- Checkout field
- Client-side validation

API:
- Accept delivery_date on cart and order operations

Backend:
- Validate available dates
- Save selection to quote and order
- Send it to fulfillment

Admin:
- Configure blackout dates
- Display delivery date on the order
```

For a new platform, that could become:

```text
Storefront component
        │
        ▼
Delivery API
        │
        ▼
Delivery service
        │
        ├── configuration database
        ├── order event consumer
        └── admin UI
```

Codex can help identify and extract those responsibilities even if the Magento implementation mixes them together.

## What prevents clean separation

Magento modules frequently couple the layers through:

- PHP blocks that contain business logic
- Templates that call models directly
- Controllers that write directly to the database
- GraphQL resolvers containing domain logic
- Observers that perform rendering or session operations
- Backend classes that depend on HTTP request state
- Admin configuration read directly from arbitrary services
- JavaScript that depends on Magento-specific page configuration
- Shared database tables with no explicit service boundary

For example, this is structurally frontend code:

```php
class DeliveryDate extends Template
```

But the block might query orders, load configuration and calculate availability. Its location does not mean its behavior is purely presentational.

## Recommended target model

For the replacement platform, define stronger boundaries than Magento does:

```text
                  ┌────────────────────┐
                  │  Storefront app    │
                  └─────────┬──────────┘
                            │ Storefront API
                  ┌─────────▼──────────┐
                  │  Commerce kernel   │
                  │  and domain APIs   │
                  └─────────┬──────────┘
                            │ events/functions
              ┌─────────────▼─────────────┐
              │ Customization services    │
              └─────────────┬─────────────┘
                            │ Admin API
                  ┌─────────▼──────────┐
                  │     Admin app      │
                  └────────────────────┘
```

A migrated customization package could have a controlled format:

```text
acme-delivery-date/
├── manifest.yaml
├── backend/
│   ├── functions/
│   ├── migrations/
│   └── tests/
├── storefront/
│   ├── components/
│   └── extensions/
├── admin/
│   ├── pages/
│   └── components/
├── api/
│   ├── openapi.yaml
│   └── events.yaml
└── migration/
    ├── magento-mapping.yaml
    └── importer.go
```

The manifest would declare capabilities rather than allowing arbitrary interception:

```yaml
name: acme-delivery-date
permissions:
  - carts:read
  - carts:write
  - orders:read

subscribes:
  - checkout.validating
  - order.created

storefront:
  slots:
    - checkout.shipping.after

admin:
  pages:
    - path: settings/delivery-dates

data:
  tables:
    - delivery_blackout_dates
```

## API strategy

Use three distinct API surfaces:

1. **Storefront API**  
   Optimized for browser and headless storefront operations.

2. **Admin API**  
   Configuration, catalog management and operational actions.

3. **Integration API**  
   Stable contracts for ERP, PIM, warehouse and marketplace systems.

Custom modules should not gain unrestricted database or in-process object access. Give them narrow permissions, versioned APIs and subscribed events.

## Implication for automated migration

A scanner can classify existing Magento customization files into:

```yaml
frontend:
  - view/frontend/templates/date.phtml
  - view/frontend/web/js/date.js

admin:
  - view/adminhtml/ui_component/delivery_dates.xml
  - etc/adminhtml/system.xml

api:
  - etc/webapi.xml
  - etc/schema.graphqls

backend:
  - Observer/SaveDeliveryDate.php
  - Model/Availability.php
  - Cron/ExpireDates.php

mixed_or_uncertain:
  - Block/DeliveryDate.php
```

Codex can then:

- Extract business logic from blocks and controllers
- Generate frontend components
- Convert API declarations
- Create backend functions or services
- Generate an admin interface
- Flag cross-layer coupling for review

Magento modules are therefore separable into these layers, and Magento's conventions provide useful signals. However, the migration process must analyze dependencies and behavior because the existing layers are often coupled. The new extension model should enforce the separation that Magento merely suggests.
