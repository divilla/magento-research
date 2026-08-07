# Magento frontend and backend boundaries

Traditional Magento is **not** designed as a clean “API backend + independent JavaScript SPA” system.

Its frontend and backend responsibilities are recognizable, but often intertwined inside one server-side PHP application.

## Traditional Magento architecture

A normal Magento storefront request looks roughly like this:

```text
Browser
   ↓
Magento PHP controller
   ↓
Blocks and view models
   ↓
Business services and models
   ↓
Server-rendered .phtml template
   ↓
HTML + Magento JavaScript
   ↓
Browser
```

The storefront uses:

- Server-rendered `.phtml` templates
- XML page layouts
- PHP blocks and view models
- RequireJS modules
- Knockout components
- jQuery
- Browser-side customer-data sections
- Backend-generated JavaScript configuration

The browser may call REST or GraphQL for particular operations, but the storefront is not necessarily an independent API consumer.

## “Backend” has two meanings

Magento terminology can be confusing:

1. **Commerce backend** — catalog, cart, orders, pricing and other domain logic.
2. **Admin backend** — the merchant-facing administration application.

Both the storefront and admin application run within the same Magento PHP installation and share:

- Dependency-injection container
- Database
- Models and services
- Configuration
- Sessions
- Events and plugins
- Module system

A Magento module can add code to both applications at once.

## Module boundaries are organizational

Magento provides recognizable directories:

```text
view/frontend/       Storefront presentation
view/adminhtml/      Admin presentation
Controller/          HTTP controllers
Model/               Domain and persistence code
Api/                 PHP service contracts
etc/webapi.xml       REST/SOAP exposure
etc/schema.graphqls  GraphQL exposure
```

But these do not enforce a clean architectural boundary.

For example:

- A PHP block used for rendering might calculate business rules.
- A template might call methods that load database entities.
- A controller might manipulate models directly.
- A GraphQL resolver might contain domain logic.
- JavaScript might depend on server-rendered configuration and session state.
- An observer might act differently depending on whether execution came from the storefront, admin, cron, REST, or GraphQL.

The folders help classify code, but they do not guarantee separation.

## Headless Magento is different

Magento can be used as an API backend:

```text
Vue/React storefront
        ↓
GraphQL and REST
        ↓
Magento commerce backend
        ↓
Database and integrations
```

Examples include custom Vue storefronts, PWA Studio and other headless implementations.

In a genuinely headless installation:

- The SPA owns routing and rendering.
- Magento exposes products, carts, customers and checkout through GraphQL or REST.
- Traditional Magento themes may be unused.
- Custom modules may expose GraphQL fields and resolvers.
- Some Magento-specific session and checkout assumptions still remain.

This is much closer to the clean separation described above. Such stores would be substantially easier to migrate if the new platform provides compatible APIs.

## Three storefront categories

For migration, stores can be classified into these categories:

| Storefront | Separation | Migration difficulty |
|---|---:|---:|
| Traditional Luma/custom Magento theme | Low | High |
| Hyvä server-rendered theme | Medium | Medium–high |
| Headless Vue/React storefront | High | Low–medium |

### Traditional Magento theme

Backend and presentation are closely coupled. The storefront usually needs to be rebuilt.

### Hyvä

Hyvä simplifies the frontend substantially, but it remains a Magento server-rendered theme using PHP templates and layout XML. It is cleaner, not fully headless.

### Headless SPA

The storefront already communicates through APIs. If the new platform reproduces the API operations it uses, the existing frontend could potentially continue running with relatively small changes.

## Implication for the replacement platform

The new architecture should make this division explicit:

```text
Vue/React storefront
        │
        │ Storefront API
        ▼
Go commerce platform
        │
        ├── Domain services
        ├── Extension runtime
        ├── Database
        └── Events
        ▲
        │ Admin API
Vue/React admin application
```

Every frontend customization should be one of:

- A storefront component
- An admin component
- A theme or design token
- An API consumer

Every backend customization should be one of:

- A domain function
- An event handler
- A workflow
- An integration service
- A data extension

Frontend components should not be permitted to access the database or internal Go services directly.

Magento therefore **distinguishes frontend, admin and API execution areas**, but traditional Magento does **not enforce the clean client/server boundary** of an API backend with an independent Vue SPA. Headless Magento does—and those installations are the easiest migration targets.
