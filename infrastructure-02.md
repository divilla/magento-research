# How Magento scales

Magento scales unevenly:

- The **web/PHP tier scales horizontally** fairly well.
- Caches, search and queues can be separated into dedicated clusters.
- The **transactional MariaDB database is the principal scaling constraint**.

Adobe's own scaled cloud architecture adds web nodes horizontally, but says its service tier—including MariaDB—primarily scales vertically by increasing CPU and memory. [Adobe scaled architecture](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/scaled-architecture)

## Typical scaled deployment

```text
                         CDN
                          │
                       Varnish
                          │
                    Load balancer
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
      PHP node 1      PHP node 2      PHP node N
          │               │               │
          └───────────────┼───────────────┘
                          │
        ┌─────────────────┼──────────────────┐
        ▼                 ▼                  ▼
 MariaDB cluster    Redis / Valkey      OpenSearch
        │            cache/session        search
        │
        └────────── RabbitMQ/ActiveMQ
                    background work
```

## Web and application tier

Magento PHP processes are mostly stateless when sessions and caches are externalized.

You can add more:

- Nginx/PHP-FPM nodes
- Queue consumers
- Cron workers
- Import workers
- GraphQL/API servers

Requirements include:

- Shared or object-based media storage
- Redis/Valkey-backed sessions
- Centralized database
- Consistent deployment artifacts
- Load balancer
- No critical state stored on local disks

This part scales relatively predictably. Adobe's cloud infrastructure can autoscale web nodes horizontally. [Adobe autoscaling](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/autoscaling)

## Read traffic

Magento reduces database reads using several layers:

```text
Browser
  ↓
CDN/Varnish           full pages
  ↓
Redis/Valkey          Magento caches and sessions
  ↓
OpenSearch            catalog search
  ↓
MariaDB               authoritative data
```

For anonymous browsing, a high cache-hit rate means many requests never reach PHP or MariaDB.

This is why a Magento store can handle a great deal of browsing traffic while still struggling during checkout or administrative bulk operations.

Database replicas may also serve reporting or selected read workloads, but asynchronous replication introduces stale-read risks. Magento and custom extensions are not universally designed to route arbitrary queries safely to replicas.

## Write traffic

Writes are more difficult:

- Cart updates
- Inventory reservations
- Order placement
- Payment state changes
- Product imports
- Admin catalog changes
- Price and promotion updates
- Indexing
- Cron bookkeeping
- Queue metadata

These converge on the relational database and require transactional consistency.

Adding PHP nodes does not help when they all contend on the same:

- Tables
- Indexes
- Rows
- Locks
- Buffer pool
- Disk I/O
- Transaction log

At that point, additional application nodes can make contention worse.

## Why MariaDB becomes the bottleneck

Magento has several database-intensive characteristics.

### EAV catalog model

Many product attributes are distributed across multiple tables:

```text
catalog_product_entity
catalog_product_entity_varchar
catalog_product_entity_int
catalog_product_entity_decimal
catalog_product_entity_text
```

Loading or updating complex products can involve numerous joins and writes.

### Materialized indexes

Magento maintains derived index tables for:

- Product prices
- Category/product relationships
- Inventory
- Search
- Promotions

These improve storefront reads but make writes and reindexing more expensive.

### Cart and order consistency

Checkout must coordinate:

- Quote
- Quote items
- Customer
- Addresses
- Inventory reservations
- Payment
- Sales order
- Events and extension logic

This creates contention around high-value transactional paths.

### Extension queries

Custom modules may:

- Run unindexed queries
- Load entities in loops
- Write during frontend requests
- Hold transactions open
- Join large EAV and sales tables
- Invalidate caches excessively

One poor extension can erase much of the benefit gained from additional infrastructure.

## Vertical database scaling

The common path is:

- More CPU
- More RAM
- Faster NVMe storage
- Larger buffer pool
- Higher IOPS
- Better query indexes
- Database connection tuning
- High-availability MariaDB topology

This works for a long time, but it has a ceiling and can become expensive.

Adobe explicitly notes that its service tier cannot reliably scale horizontally using its current technologies and instead scales by selecting larger nodes. [Adobe scaled architecture](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/scaled-architecture)

## Database sharding

Magento does not provide general-purpose, transparent sharding by:

- Customer
- Store
- Product
- Order
- Region

Adobe Commerce previously offered a split-database feature separating main, checkout and sales databases, but it was deprecated in Magento 2.4.2. Magento Open Source used only one primary database in that design. [Adobe split-database documentation](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/split-db/multi-master)

Custom sharding is possible, but it breaks assumptions made by:

- SQL joins
- Foreign keys
- Transactions
- Extensions
- Reports
- Admin grids
- Setup scripts

It would be closer to rewriting Magento's persistence layer than configuring it.

## Background processing

Magento improves request performance by moving work into queues:

```text
HTTP request
    ↓
Commit essential transaction
    ↓
Publish message
    ↓
Return response

Queue consumer
    ↓
ERP export / email / indexing / feed generation
```

Queue consumers scale horizontally when messages are independent and idempotent.

However, they frequently write results back into MariaDB, so increasing workers can eventually create database contention.

## Traffic types scale differently

| Workload | Scaling characteristics |
|---|---|
| Cached anonymous browsing | Excellent |
| Search and category browsing | Good with OpenSearch and caching |
| Headless product queries | Good if responses are cached |
| Authenticated browsing | Moderate |
| Cart updates | Database-dependent |
| Checkout and order placement | Database-intensive |
| Bulk catalog import | Database and indexing-intensive |
| Reindexing | CPU, memory, I/O and DB intensive |
| Admin reporting | Potentially very expensive |
| Queue processing | Horizontal until the DB becomes limiting |

## Implication for a Go replacement

A Go rewrite would reduce application-server overhead, but it would not automatically solve database scaling if it retained:

- The same schema
- EAV query patterns
- Global transactions
- Synchronous integrations
- Centralized writes

A replacement architecture should deliberately introduce domain ownership:

```text
Catalog database       Product and category data
Pricing engine         Prices and promotions
Inventory database     Stock and reservations
Cart store             Short-lived cart state
Order database         Durable sales records
Search index           Query-optimized product documents
Event log/queue        Cross-domain propagation
```

This creates independent scaling boundaries, though it introduces eventual consistency and distributed-system complexity.

Magento scales well for cached storefront traffic and can scale its application tier horizontally, but its transactional database predominantly scales vertically. Database contention, indexing and synchronous extension behavior become the practical ceiling.
