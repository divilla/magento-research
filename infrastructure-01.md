# Magento database and persistence infrastructure

Magento uses a **MySQL-compatible relational database** as its primary transactional store:

- Historically: **MySQL**
- Current Magento/Adobe Commerce releases: primarily **MariaDB**
- Some supported versions and environments also use **MySQL or Amazon Aurora MySQL**

As of the current 2026 requirements:

- Adobe Commerce 2.4.9 supports **MariaDB 11.8/12.3**
- Adobe Commerce 2.4.8 supports **MariaDB 11.4/11.8**
- Older supported release lines generally use MariaDB 10.6 or 10.11
- MySQL 8.0 reached end of support in April 2026, so Adobe recommends compatible MariaDB versions for affected installations. [Adobe system requirements](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements)

## What it stores

The relational database holds:

- Products, categories and attributes
- Customers and addresses
- Carts and quotes
- Orders, invoices, shipments and refunds
- Prices, promotions and tax configuration
- Inventory and reservations
- Store configuration
- CMS content
- Admin users and permissions
- Extension-owned tables
- Cron and queue metadata

Magento uses InnoDB-style transactions, foreign keys, indexes, temporary tables and database triggers in some indexing workflows.

## Other persistence services

These complement the primary database:

- **OpenSearch** — catalog search and some indexed queries
- **Redis or Valkey** — cache and sessions
- **RabbitMQ/ActiveMQ** — asynchronous messages
- **Filesystem or object storage** — product media, generated files and imports
- **Varnish** — full-page HTTP cache

For a replacement project, the authoritative source is usually MariaDB/MySQL, but behavioral state can also exist in search indexes, caches, queues, sessions and files. A complete compatibility harness must observe all of them—not only SQL tables.
