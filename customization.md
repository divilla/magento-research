# How Magento is customized

Magento is customized primarily through **modules, themes, configuration, and integrations**. Core files should not be edited directly, because upgrades would overwrite those changes.

## 1. Custom modules

A module adds or changes business logic. It typically lives under:

```text
app/code/Vendor/Module/
├── registration.php
├── etc/module.xml
├── etc/di.xml
├── Controller/
├── Model/
├── Plugin/
├── Observer/
├── Api/
└── view/
```

Modules can add:

- Checkout rules
- Payment and shipping methods
- Product attributes
- Admin screens
- API endpoints
- Scheduled jobs
- Database tables
- Pricing and promotion logic

## 2. Plugins and observers

Magento provides two important extension mechanisms:

- **Plugins/interceptors** run before, after, or around a public PHP method.
- **Observers** respond to dispatched events, such as an order being placed.

For example, a plugin could adjust a product price after Magento calculates it. An observer could notify an ERP when an order is submitted.

Plugins are powerful, but `around` plugins should be used sparingly because they can disrupt execution and conflict with other extensions.

## 3. Dependency injection and class replacement

Magento's dependency-injection configuration, usually `etc/di.xml`, controls which classes implement particular interfaces.

A **preference** can replace an entire class:

```xml
<preference for="Magento\Catalog\Api\ProductRepositoryInterface"
            type="Vendor\Module\Model\ProductRepository"/>
```

This is generally a last resort. Plugins, composition, and service contracts usually produce fewer conflicts.

## 4. Themes and storefront code

Themes control the presentation layer:

```text
app/design/frontend/Vendor/theme/
├── theme.xml
├── registration.php
├── Magento_Catalog/
├── Magento_Checkout/
├── web/css/
├── web/js/
└── templates/
```

A theme can customize:

- Page layouts
- `.phtml` templates
- CSS and JavaScript
- Email templates
- Product and category pages
- Checkout presentation

Traditional Magento themes use XML layouts, `.phtml`, LESS, RequireJS, and Knockout. Alternatives such as Hyvä replace much of that frontend stack, while headless implementations use Magento through GraphQL or REST.

## 5. Admin configuration

A surprising amount can be customized without writing code:

- Store views, languages, and currencies
- Tax and shipping rules
- Catalog structure
- Customer groups
- Promotions
- Transactional emails
- CMS pages and blocks
- Payment configuration

Configuration can be scoped globally, per website, or per store view.

## 6. Third-party extensions

Extensions are installed through Composer and enabled as Magento modules:

```bash
composer require vendor/package
bin/magento module:enable Vendor_Module
bin/magento setup:upgrade
```

They commonly add payments, shipping, search, SEO, feeds, analytics, and marketplace functionality. Extension compatibility is one of Magento's bigger maintenance risks.

## 7. External integrations

Magento is frequently connected to:

- ERP and accounting systems
- PIMs
- CRMs
- Warehouse systems
- Payment providers
- Search engines
- Marketplaces
- Marketing platforms

Integrations use REST, GraphQL, asynchronous queues, webhooks, scheduled imports, or custom APIs.

In short, Magento customization is less like editing a website and more like extending an application framework. A typical serious Magento store combines a custom theme, several custom modules, dozens of third-party modules, and multiple external integrations.
