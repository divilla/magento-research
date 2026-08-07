# Behavioral compatibility testing before replacing Magento

This is a viable strategy. What is being described is a **behavioral compatibility harness** around Magento. Once that harness is sufficiently complete, Magento can be replaced component by component while treating the original system as the behavioral oracle.

The important correction is:

> You cannot prove coverage of “all edge cases,” but you can systematically cover all known behaviors, extension points, state transitions, integrations, and production-observed scenarios.

That can be strong enough to begin translation safely.

## Magento as an observable state machine

Do not frame tests only as GET and POST endpoint tests. Frame every operation as:

```text
Initial state
    +
Input/action
    ↓
Magento execution
    ↓
Observable result
    +
Final state
    +
Side effects
```

For example:

```yaml
scenario: partial_refund_with_discount_and_tax

initial_state:
  order:
    products: [simple, configurable]
    discount: fixed_cart
    tax_mode: prices_including_tax
    shipment: partially_shipped

action:
  actor: admin
  operation: create_credit_memo
  refund_items:
    simple-sku: 1

expected:
  response: success
  order_state: processing
  refunded_total: 42.37
  inventory_changes:
    simple-sku: +1
  records_created:
    - credit_memo
  events:
    - creditmemo_save_after
  messages:
    - refund_requested
  payment_gateway:
    refund_amount: 42.37
```

The same fixture should later run against the Go implementation.

## Inputs that must be covered

### Storefront/browser actions

- Page requests
- Forms
- AJAX requests
- Customer registration and authentication
- Cart operations
- Checkout
- Payment redirects and callbacks
- Customer account actions
- Cookies and sessions
- CSRF behavior
- File uploads
- Store and currency switching

For traditional Magento, use real browser tests because JavaScript, cookies, generated form keys, Knockout state, and server-rendered forms matter.

### Admin actions

- Authentication and authorization
- Catalog management
- Order creation and editing
- Invoicing, shipping and refunds
- Configuration changes
- Customer management
- Imports and exports
- Grid filters and mass actions
- Extension-provided admin screens
- Store-scoped configuration
- ACL restrictions

Admin behavior is just as important as storefront behavior because merchants may depend on subtle workflows.

### APIs

- REST
- GraphQL
- Asynchronous REST
- SOAP, if used
- Custom controllers
- Payment and shipping callbacks
- Webhooks
- ERP and PIM endpoints

### Non-HTTP entry points

Magento also executes through:

- Cron
- Queue consumers
- CLI commands
- Indexers
- Setup and data patches
- Import jobs
- Filesystem ingestion
- Email processing
- External callbacks
- Direct database integrations
- Scheduled ERP synchronization

These must be modeled as explicit triggers.

## Outputs that must be observed

An HTTP response alone does not establish whether behavior matches.

Capture:

- Response status, headers and body
- Browser DOM and important UI state
- Database changes
- Order and entity state transitions
- Generated emails
- Published queue messages
- Consumed queue messages
- Events and observers invoked
- External HTTP calls
- Payment and shipping requests
- Files created or modified
- Logs and exceptions
- Cache invalidation
- Indexer changes
- Inventory reservations
- Search-index documents
- Cron schedule changes

The harness needs adapters that observe or virtualize these outputs.

## Record Magento, then replay

The strongest design is a differential-testing system:

```text
                         ┌── Magento ──────── result A
Scenario + initial state ┤
                         └── New platform ─── result B
                                              │
                                              ▼
                                      Semantic comparator
```

Magento acts as the reference implementation.

The comparator should not blindly compare raw outputs. IDs, timestamps, hashes, generated tokens and ordering may differ. Normalize them first:

```json
{
  "entity_id": "<generated>",
  "created_at": "<timestamp>",
  "increment_id": "<order-number>",
  "grand_total": "129.90",
  "state": "processing"
}
```

Then compare business semantics.

## Build a canonical scenario format

Use one implementation-neutral test definition:

```yaml
name: guest-checkout-free-shipping-coupon

store:
  code: default
  currency: EUR

fixtures:
  products:
    - sku: SHIRT
      price: 80
      quantity: 10
  promotion:
    code: FREESHIP
    condition: cart_total_above_50

steps:
  - storefront.create_guest_cart
  - storefront.add_product:
      sku: SHIRT
      quantity: 2
  - storefront.apply_coupon:
      code: FREESHIP
  - storefront.set_shipping_address:
      fixture: croatian_address
  - storefront.select_shipping_method:
      code: standard
  - storefront.place_order:
      payment: fake_card

assert:
  order:
    subtotal: 160.00
    shipping: 0.00
    status: processing
  inventory:
    SHIRT: 8
  payment:
    captured: 160.00
```

Implement two drivers:

```text
MagentoDriver
GoPlatformDriver
```

Both execute the same scenario.

This prevents the test suite from becoming coupled to Magento's implementation.

## Use controlled substitutes for external systems

Never make compatibility testing depend on live payment, ERP or shipping services.

Provide emulators for:

- Payment gateways
- Shipping carriers
- Tax services
- ERP
- PIM
- Email
- Object storage
- Search
- Message broker
- Webhooks

They should record requests and provide programmable responses:

```yaml
payment_gateway:
  on_authorize:
    respond:
      status: declined
      code: insufficient_funds
```

You can then test failures, timeouts, malformed responses, duplicate callbacks and retries deterministically.

## Where scenarios come from

A comprehensive suite should combine several sources.

### Requirements and documentation

Establish intentional expected behavior.

### Code and configuration analysis

Discover:

- Controllers
- REST and GraphQL routes
- Observers
- Plugins and preferences
- Cron jobs
- Queue consumers
- CLI commands
- Admin actions
- Configuration branches
- Exceptions and validation rules

This identifies scenarios that may not appear in documentation.

### Production traffic

Sanitized production traces reveal behaviors that developers did not anticipate:

- Real product combinations
- Customer-group differences
- Rare promotion interactions
- Payment callback sequences
- ERP anomalies
- Unusual admin workflows

Convert traces into replayable regression scenarios.

### Data profiling

Inspect production-shaped data for:

- Attribute combinations
- Product types
- Order states
- Store views
- Customer groups
- Tax classes
- Promotion types
- Inventory sources
- Historical anomalies

Tests built only on synthetic clean data will miss important behavior.

### Generative and property-based testing

Generate combinations around invariants:

```text
Order grand total must equal:
items + tax + shipping + fees - discounts
```

Other properties:

- Inventory cannot silently disappear.
- A successful idempotent callback cannot create two payments.
- A refund cannot exceed the captured amount.
- Replaying a message cannot duplicate an order.
- Unauthorized administrators cannot perform restricted actions.
- Cart totals should remain stable across recalculation without state changes.

## Why “all edge cases” is impossible

The possible state space is enormous:

```text
product types
× customer groups
× websites and store views
× currencies
× tax configurations
× promotions
× shipping methods
× payment methods
× inventory sources
× extension combinations
× order states
× failure timings
```

Concurrency adds more combinations:

- Two customers buying the last unit
- Duplicate payment callbacks
- A refund racing with shipment creation
- Indexing during a catalog update
- Queue messages arriving out of order

No finite integration suite can mathematically prove every combination.

Instead, define sufficiency using several measurable dimensions:

- Every entry point exercised
- Every business state transition exercised
- Every custom module exercised
- Every external integration exercised
- Every configured product type exercised
- Every active store/customer/tax scope exercised
- Every important error path exercised
- Every production-observed scenario represented
- High-risk pairwise combinations exercised
- Critical invariants fuzzed
- Mutation testing demonstrates that tests detect behavioral changes

## Mutation testing is especially valuable

Coverage can lie. A test may execute a line without checking its result.

Deliberately mutate Magento or a compatibility model:

- Reverse a condition
- Remove a discount
- Skip an observer
- Change rounding
- Disable inventory reservation
- Suppress a queue message
- Bypass an ACL check

If the suite still passes, it does not adequately characterize that behavior.

Mutation testing tells you whether the harness is sensitive enough to catch an incorrect translation.

## When translation can begin

You do not need to finish the entire harness before translating anything. Establish a gate for each bounded domain:

```text
Catalog test coverage sufficient
        ↓
Translate catalog
        ↓
Run Magento vs Go differential suite
        ↓
Catalog accepted
```

A domain is ready when:

1. Inputs and outputs are inventoried.
2. Current behavior is captured.
3. External systems are virtualized.
4. Important state transitions have scenarios.
5. Production-relevant data fixtures exist.
6. Mutation testing shows meaningful sensitivity.
7. Both implementations can execute the same scenarios.
8. Differences are classified and approved.

Then replace domains incrementally:

```text
Catalog → Customers → Pricing → Cart
→ Inventory → Checkout → Orders → Admin
```

The exact order may differ because pricing, inventory, and cart behavior are tightly connected.

## The admin interface complicates equivalence

There are two choices.

### Preserve workflow equivalence

Build a new admin interface whose user workflows behave similarly:

- Same capabilities
- Similar validation
- Equivalent permissions
- Equivalent state transitions

Tests assert outcomes, not identical HTML.

### Preserve exact interface compatibility

Replicate selectors, routes, form structure and screen behavior closely enough that existing browser automation continues working.

This is far more expensive and generally unnecessary. Preserve business workflows rather than Magento's admin markup.

## How Codex can help

Codex can accelerate:

- Entry-point discovery
- Scenario generation
- Fixture builders
- Browser and API test implementation
- External-service fakes
- Database-state extractors
- Output normalization
- Differential comparators
- Property tests
- Translation of isolated domains
- Investigation of mismatches

Codex should operate inside the harness. The trustworthy loop is:

```text
Codex translates behavior
        ↓
Compatibility suite finds differences
        ↓
Codex investigates and corrects them
        ↓
Human reviews intentional deviations
```

The suite—not Codex's confidence—is the acceptance authority.

## Bottom line

This approach can work and is probably the safest way to replace Magento without a one-to-one rewrite.

The first product would effectively be a **Magento behavioral specification and differential-testing platform**. Once it can:

- reset both systems to equivalent state,
- execute the same storefront, admin, API and background scenarios,
- capture all important side effects,
- and compare normalized outcomes,

Magento can be translated domain by domain with a credible safety net.

Every theoretical edge case can never be known to be covered. But it is possible to reach a defensible point where every known entry point, production behavior, state transition, customization and failure class is represented—and where new discoveries become permanent regression tests.
