# How controlled are Magento customizations?

You can reliably expect a **standard module envelope**, but you cannot expect the customization itself to follow a small number of controlled behavioral formats.

A useful way to think about it:

> Magento standardizes how customizations are discovered and connected, but not what they can do once connected.

## What is reliably standardized

A conventional Magento 2 module will normally be found in one of these locations:

```text
app/code/Vendor/Module/
vendor/vendor-name/module-name/
```

Its minimum recognizable structure is usually:

```text
Vendor/Module/
├── registration.php
├── composer.json
└── etc/
    └── module.xml
```

Adobe documents `registration.php`, `composer.json`, and the component-specific XML file as the required component files. Magento also expects configuration in predefined locations. [Adobe component structure](https://developer.adobe.com/commerce/php/development/prepare/component-file-structure/)

That means a scanner can reliably determine:

- Module name
- Composer package
- Namespace and source path
- Declared dependencies
- Whether the module is enabled
- Module load order
- Which conventional Magento extension points it declares

## Common recognizable formats

Most well-behaved modules expose their entry points through XML files under `etc/`.

| File or location | Meaning |
|---|---|
| `etc/module.xml` | Module identity and load order |
| `etc/di.xml` | Plugins, preferences and dependency injection |
| `etc/events.xml` | Global event observers |
| `etc/frontend/events.xml` | Storefront observers |
| `etc/adminhtml/events.xml` | Admin observers |
| `etc/crontab.xml` | Scheduled jobs |
| `etc/webapi.xml` | REST/SOAP endpoints |
| `etc/graphql/` and schema files | GraphQL behavior |
| `etc/db_schema.xml` | Declarative database schema |
| `Setup/Patch/` | Schema and data patches |
| `Controller/` | HTTP controllers |
| `Console/` | CLI commands |
| `Plugin/` | Interceptors |
| `Observer/` | Event handlers |
| `Cron/` | Scheduled-job implementations |
| `Api/` | Service contracts |
| `view/` | Templates, layouts, JS and CSS |
| `Ui/` | Admin grids and forms |
| `etc/adminhtml/system.xml` | Admin configuration |
| `etc/acl.xml` | Permissions |
| `etc/queue*.xml` | Message queues and consumers |

Adobe explicitly defines many of these as common module directories and configuration locations. [Adobe module file structure](https://developer.adobe.com/commerce/php/development/build/component-file-structure), [configuration files](https://developer.adobe.com/commerce/php/development/build/required-configuration-files)

This makes **structural classification highly automatable**.

## Where control ends

An observer has a predictable declaration:

```xml
<event name="sales_order_place_after">
    <observer
        name="acme_export_order"
        instance="Acme\Export\Observer\ExportOrder"/>
</event>
```

Its class also has a predictable interface:

```php
class ExportOrder implements ObserverInterface
{
    public function execute(Observer $observer)
    {
        // Arbitrary PHP begins here.
    }
}
```

Magento controls the declaration and `execute()` entry point. Inside that method, the module can:

- Update any database table
- Load arbitrary Magento services
- Call an external ERP
- Write files
- Start subprocesses
- Dispatch more events
- Send email
- Modify global state
- Execute raw SQL
- Call undocumented module internals

Adobe's observer documentation defines the XML declaration and interface, but observers remain dynamically injected PHP code capable of changing application behavior. [Adobe events and observers](https://developer.adobe.com/commerce/php/development/components/events-and-observers/)

The same applies to plugins. Their declaration and `before`, `after`, or `around` conventions are standardized, but their implementation is arbitrary PHP. [Adobe plugin documentation](https://developer.adobe.com/commerce/php/development/components/plugins)

## The least controlled mechanisms

Some customizations are considerably harder to analyze.

### Preferences

A preference replaces an entire class implementation:

```xml
<preference
    for="Magento\Catalog\Model\Product"
    type="Acme\Catalog\Model\Product"/>
```

The replacement may change almost anything the original class does.

### Around plugins

An `around` plugin controls whether and how the original method is called. It can effectively replace the operation.

### Class inheritance

Custom classes can extend internal Magento classes and override protected behavior without declaring every changed behavior in XML.

### Direct Object Manager use

Code can dynamically request classes:

```php
$objectManager->get($className);
```

If the class name is calculated at runtime, static analysis becomes less reliable.

### Dynamic configuration

Class names, event names, API URLs and behavior can come from:

- Database configuration
- Environment variables
- Store-scoped settings
- Serialized data
- External services

### Database manipulation

Modules may use:

- Declarative `db_schema.xml`
- Modern schema/data patches
- Legacy install and upgrade scripts
- Raw SQL issued from arbitrary PHP

Magento has supported multiple database migration generations, so a scanner must understand all of them. [Adobe declarative-schema history](https://developer.adobe.com/commerce/php/development/components/declarative-schema/configuration)

### Frontend code

JavaScript is especially unconstrained. A module can use:

- RequireJS mixins
- Knockout components
- UI components
- Inline JavaScript
- jQuery plugins
- Template overrides
- Layout XML
- Third-party bundles

### Core patches and off-module changes

Badly maintained stores sometimes include:

- Modified files under `vendor/`
- Composer patches
- Changes to Magento core
- Root-level scripts
- Web-server configuration changes
- Custom cron commands outside Magento
- Integrations that are not present in the repository

These may not appear as modules at all.

## Expected level of control

Magento customizations can be divided into three layers.

### Layer 1: Mechanically discoverable

Usually very reliable:

- Installed and enabled modules
- Composer packages
- XML declarations
- Events and plugins
- Preferences
- Cron jobs
- API routes
- Database schemas
- Configuration fields
- Layout and template overrides

A scanner should achieve close to complete coverage here for conventional modules.

### Layer 2: Statically understandable

Often recoverable with Codex and static analysis:

- Data read and written
- Services called
- HTTP requests
- Event payload usage
- Business conditions
- Dependencies on Magento classes
- Likely side effects

Confidence decreases with dynamic PHP, factories, runtime configuration and generated class names.

### Layer 3: Behaviorally verifiable

Requires executing the system:

- Actual order-total changes
- Extension interaction and plugin ordering
- Store-scoped differences
- Retry and failure behavior
- External integration semantics
- Hidden dependencies on production data
- Frontend behavior

Static inspection alone cannot guarantee these.

## What this means for a migration product

You can build a dependable parser around a finite collection of **module entry-point formats**. You cannot build a dependable migration system using file patterns alone.

The analyzer should combine:

```text
Module discovery
      ↓
XML and Composer parsing
      ↓
PHP dependency and call-graph analysis
      ↓
Codex semantic analysis
      ↓
Runtime instrumentation
      ↓
Behavioral replay tests
```

Each finding should retain evidence:

```yaml
customization:
  type: observer
  declaration: app/code/Acme/Export/etc/events.xml
  class: Acme\\Export\\Observer\\ExportOrder
  trigger: sales_order_place_after
  writes:
    - acme_export_queue
  external_calls:
    - config: acme_erp/general/base_url
  confidence:
    discovery: high
    semantic_behavior: medium
    runtime_verified: false
```

In summary:

- **Yes**, you can consistently discover and classify properly packaged Magento modules.
- **Yes**, most extension mechanisms come from a finite, documented set.
- **No**, their internal behavior is not sandboxed or declarative.
- **No**, you cannot assume all customization lives in modules.
- **Therefore**, automated migration is feasible, but it needs static analysis, semantic code analysis, and runtime validation—not merely format conversion.
