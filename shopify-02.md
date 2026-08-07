# What can be taken from Magento during a Shopify migration?

“Data and templates” is directionally correct, but **templates are usually not actually portable**. A better description is:

> You transfer data, content, media, domains, and business knowledge. You rebuild or replace almost everything executable.

## What can genuinely be transferred

### Commerce data

- Products, SKUs, and variants
- Categories, translated into Shopify collections
- Prices and inventory values
- Customers and addresses
- Historical orders and transactions
- Reviews, wish lists, and loyalty balances, usually through apps or custom APIs
- Gift-card and store-credit balances, with limitations
- Product attributes, translated into options, tags, or metafields

Some Magento structures do not map one-to-one. Configurable, bundle, grouped, and custom product types may need to be remodelled.

### Content and assets

- Product descriptions
- CMS pages and blog posts
- Images, videos, PDFs, and downloadable files
- Navigation structure
- Email wording
- Brand assets, fonts, icons, and design files
- SEO titles, descriptions, and structured-content values

### Digital continuity

- Domain names
- URL inventory and redirect mappings
- Analytics identifiers and historical analytics data
- Tracking specifications
- Search Console ownership
- Merchant Center feeds and advertising-account configuration
- Email sender domains
- Existing consent and customer-marketing status, subject to legal and platform constraints

The redirect map is particularly valuable. Magento and Shopify use fundamentally different URL structures, so indexed Magento URLs normally require explicit 301 mappings. Shopify’s [migration documentation](https://help.shopify.com/en/manual/migrating-to-shopify) identifies products, customers, orders, gift cards, blogs, and pages as transferable data.

## What can be reused only indirectly

### Visual design

Magento `.phtml`, layout XML, RequireJS, Knockout, LESS, and module frontend code cannot become a Shopify theme. Shopify themes use Liquid, JSON templates, sections, and its own JavaScript conventions.

You can reuse:

- Visual design
- CSS selectively
- Images, fonts, and icons
- Component specifications
- Responsive behaviour
- Accessibility requirements
- Figma and design-system assets

The actual theme normally needs to be rebuilt. Calling this “template migration” can therefore understate the work.

### Business rules

These are often the most valuable things extracted from Magento:

- Promotion and coupon rules
- Customer-group pricing
- Tax logic
- Shipping eligibility
- Inventory and back-order behaviour
- Product visibility rules
- Order state transitions
- Approval and quote workflows
- Returns and cancellation policies
- Fraud rules
- Regional restrictions

The Magento implementation cannot normally be transferred, but its behaviour can be documented and then implemented using Shopify configuration, Shopify Functions, Flow, apps, or external services.

### Integrations

The underlying relationships can survive:

- ERP
- PIM
- OMS/WMS
- CRM
- Search
- Tax
- Payment providers
- Shipping services
- Marketing automation
- Reviews and loyalty systems

Magento extension code and observers cannot run on Shopify. Each integration needs a new Shopify connector, app, middleware adapter, or API implementation. Configuration and mapping knowledge may be reusable; the code generally is not.

## What usually cannot be taken directly

- Magento PHP modules
- Database schema and custom tables as functioning application structures
- Magento admin customizations
- Cron jobs and message-queue consumers
- Checkout overrides
- Indexers and cache logic
- Magento ACL roles and permissions
- Extension licenses
- Payment tokens unless both processors support a compliant vault migration
- Existing customer passwords in most cases
- Sessions, carts, and active checkout state
- Native Magento search indexes
- Exact order-state and workflow semantics
- Magento theme templates

Customer password hashes are a notable issue: customers commonly need to activate the new account or reset their password. Payment credentials are even more sensitive and generally require a processor-managed, PCI-compliant transfer rather than a database export.

## A more accurate migration model

| Layer | Treatment |
|---|---|
| Products, customers, orders, content | Transfer and transform |
| Media and brand assets | Copy |
| SEO authority | Preserve through redirects and metadata |
| Theme | Rebuild |
| Business rules | Rediscover and reimplement |
| Extensions | Replace or retire |
| Integrations | Reconnect or rewrite |
| Infrastructure and platform operations | Abandon; Shopify assumes them |
| Obsolete customizations | Deliberately discard |

The tangible payload is larger than data and templates—but the valuable additional material is often **knowledge rather than code**: rules, mappings, integration contracts, operational processes, SEO history, and exception handling.

For a simple store, migration can mostly be data plus a new theme. For a mature Magento installation, the harder part is usually discovering which behaviour is hidden in extensions, custom modules, cron jobs, ERP integrations, and years of operational exceptions.
