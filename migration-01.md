# A Magento-compatible migration destination

The goal does not need to be rewriting Magento. It can instead be building a **Magento-compatible migration destination**.

The product promise becomes:

> Move your Magento store without rebuilding your catalog, integrations, storefront, and business rules from scratch.

The key is compatibility at the migration boundaries—not compatibility with Magento's internal PHP architecture.

## What must migrate cleanly

A migration tool should connect directly to Magento and import:

- Websites, stores, store views and currencies
- Products, variants, attributes and attribute sets
- Categories and media
- Inventory and source assignments
- Customers, addresses and customer groups
- Orders, invoices, shipments, refunds and credit memos
- Tax rules
- Shipping configuration
- Coupons, promotions and price rules
- CMS pages and blocks
- URL rewrites and SEO metadata
- Configuration values
- Relevant extension-owned data

Preserve Magento IDs in dedicated `legacy_id` fields. That makes incremental synchronization, debugging and reconciliation much easier.

## Migration should be continuous

A one-time database import is insufficient because merchants cannot stop taking orders for days.

Use a staged migration:

```text
Initial bulk import
        ↓
Continuous change synchronization
        ↓
Merchant validates new store
        ↓
Short checkout freeze
        ↓
Final synchronization
        ↓
DNS/API cutover
```

Ideally, the merchant can rehearse this process multiple times. The migration must be idempotent: rerunning it should update records rather than create duplicates.

## Compatibility surfaces

### 1. Data compatibility

Build a Magento connector using its APIs and, where necessary, direct read-only database access.

Internally, use a cleaner model. Do not reproduce Magento's EAV database design. The migration layer translates EAV attributes into typed product fields and flexible custom attributes.

Provide reconciliation reports:

```text
Products       48,291 / 48,291
Customers     183,402 / 183,402
Orders        527,110 / 527,110
Media files    97,201 / 97,203   2 errors
Coupons         1,412 / 1,412
```

Trust in those reports will be a major part of the product.

### 2. API compatibility

Supporting the most frequently used Magento REST and GraphQL endpoints would dramatically simplify migrations.

You do not need every endpoint. Start with those used by:

- Storefronts
- ERP and PIM integrations
- Order synchronization
- Inventory updates
- Product imports
- Customer service tools

A compatibility gateway could translate Magento-shaped requests into the new platform's API:

```text
Existing ERP
    │ Magento REST request
    ▼
Compatibility gateway
    │ Native command
    ▼
New Go platform
```

This allows integrations to keep running while customers migrate them gradually.

### 3. Storefront compatibility

Trying to run Magento themes would drag the old frontend architecture into the new product. Instead, offer two paths:

- Keep an existing headless storefront by supporting compatible GraphQL operations.
- Automatically create a new storefront from a maintained theme.

Traditional Luma themes cannot be migrated reliably through automation. Their content, styling tokens, media and page structure can be imported, but custom templates and JavaScript will require conversion.

Hyvä compatibility could be a particularly useful target, although it would still require a deliberate adapter or frontend migration strategy.

### 4. Extension replacement

Extensions are probably the largest commercial obstacle. Merchants buy outcomes, not extensions, so map each extension to a capability:

| Magento extension | Migration destination |
|---|---|
| Payment module | Native payment connector |
| Shipping module | Native carrier connector |
| Search extension | Built-in search service |
| Product feed | Feed integration |
| SEO extension | Native SEO capability |
| ERP connector | Integration service |
| Checkout customization | Checkout configuration or custom app |
| Bespoke business logic | Event-driven external app |

Create an automated extension inventory that classifies each installed module:

- Supported natively
- Replacement available
- Data migratable
- Custom implementation required
- Blocks migration

That assessment could itself become a lead-generation product.

## Custom business logic

Do not attempt to run Magento PHP modules inside Go. Offer a controlled customization model:

- Webhooks
- Event subscriptions
- Versioned APIs
- Checkout and pricing functions
- Workflow rules
- External apps
- Possibly sandboxed WebAssembly functions

For common Magento plugins, build migration recipes. For example:

```text
Magento observer:
sales_order_place_after
        ↓
New platform event:
order.placed
        ↓
Webhook or Go/Wasm function
```

A merchant's custom module can then be translated conceptually instead of ported line by line.

## The best initial customer

Do not begin with the most complex Adobe Commerce installations. They may have hundreds of modules, B2B contracts and deeply coupled ERP systems.

A strong initial target would be:

- Magento Open Source 2 stores
- Approximately €1M–€20M in annual online revenue
- Standard products or manageable variants
- 5–30 significant extensions
- One primary storefront
- Frustrated by upgrades, performance or agency costs
- No highly specialized Adobe Commerce B2B requirements

These stores have enough pain and budget to migrate, without requiring complete Magento equivalence.

## A credible first product

The first version would need:

1. Catalog, inventory, customers and orders
2. Cart, checkout, taxes, shipping and payments
3. A functional administration interface
4. Magento bulk importer
5. Incremental synchronization
6. Redirect and SEO migration
7. Stripe or Adyen plus several regional payment options
8. A modern reference storefront
9. Webhooks and integration APIs
10. Migration validation reports

Avoid building a general marketplace initially. Implement replacements for the 20–30 capabilities that appear most frequently in target stores.

## The real moat

The Go commerce engine alone would not be the defensible asset. The moat would be:

- Reliable Magento discovery and auditing
- Automated data migration
- Magento API compatibility
- Extension replacement intelligence
- Business-rule conversion tooling
- Rehearsable, low-downtime cutover
- Proven migration playbooks

This suggests a sharper positioning:

> A modern commerce platform with a Magento exit ramp built in.

That is much more achievable than rewriting Magento and much more valuable than offering another generic commerce platform. The migration system should be treated as a first-class product, not a one-off professional service.
