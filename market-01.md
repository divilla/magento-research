# Magento adoption and platform abandonment data

Yes—but only as third-party estimates of merchant websites, not authoritative customer or churn figures from Adobe.

The best public source I found is [Store Leads’ Magento report](https://storeleads.app/reports/magento), updated July 24, 2026:

- Approximately **106,095 live Magento stores** detected.
- Store count was reportedly **down 14% year over year** in Q2 2026.
- During the previous 90 days:
  - **988 stores moved to Magento** from another detected platform.
  - **1,576 stores moved away from Magento** to another detected platform.
  - That represents a **net migration loss of 588 stores** among identifiable platform switches.

The most common detected migrations in that 90-day window were:

| Direction | Platform | Stores |
|---|---:|---:|
| Magento → Shopify | Shopify | 455 |
| Magento → WooCommerce | WooCommerce | 244 |
| Magento → BigCommerce | BigCommerce | 26 |
| Magento → Shopware | Shopware | 25 |
| Shopify → Magento | Shopify | 88 |
| WooCommerce → Magento | WooCommerce | 129 |
| Custom platform → Magento | Custom cart | 557 |

The longer-term Store Leads series shows detected active stores peaking around **163,700 in late 2022**, versus roughly **111,300 in Q2 2026**—a decline of about **32% from that peak**.

[BuiltWith](https://trends.builtwith.com/shop/Magento) provides another public dataset. It currently detects approximately **128,600 live Magento websites** and about **633,900 historical users**. Its gains/losses tables also indicate that Shopify and WooCommerce are the most common platforms associated with Magento departures. However, BuiltWith’s headline migration numbers cover its entire tracking history, not a recent annual period, so they should not be interpreted as annual churn.

## Important limitations

- These figures count **websites/storefronts, not companies or subscriptions**. One merchant can operate many domains.
- Technology detection is imperfect, particularly with headless storefronts, redirects, staging sites, and heavily customized installations.
- “Disappeared” does not necessarily mean “migrated”; the business may have closed, merged domains, or blocked detection.
- The datasets generally combine **Magento Open Source and Adobe Commerce** or cannot reliably distinguish them.
- Adobe does not appear to publicly disclose regular figures for **new Adobe Commerce customers, merchant churn, or platform migrations**.
- If “users” means shoppers creating accounts on Magento stores, there is no ecosystem-wide public dataset for that either; those records belong to individual merchants.

The defensible conclusion is: **public web-observation data shows Magento losing more storefronts than it gains, with Shopify the largest identifiable destination, but there is no audited public Magento customer-churn figure.**
