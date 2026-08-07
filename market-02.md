# Reliability of public Magento migration data

The previously presented numbers should not be treated as verified merchant migrations. They are **website-technology detections**, not observations of a merchant's actual replatforming project.

A Magento → Shopify migration is technically possible and common enough: products, customers, orders, URLs, and other data are exported or transferred through APIs or migration tools, while the storefront and integrations are rebuilt in Shopify. However, the public dataset does **not observe that business process**. It only observes that a domain previously exhibited Magento signatures and now exhibits Shopify signatures.

## Sources used

The recent migration numbers came from [Store Leads’ Magento report](https://storeleads.app/reports/magento):

- 455 domains detected as changing from Magento to Shopify within 90 days.
- 88 detected in the opposite direction.
- 1,576 detected leaving Magento for any recognized platform.
- 988 detected arriving from another recognized platform.

Store Leads says its dataset is:

- Collected by crawling public webpages.
- Refreshed weekly.
- Stored as historical snapshots going back to 2019.
- Supplemented by heuristics involving historical DNS data.

See its [data methodology overview](https://storeleads.app/alternative-data) and [platform-change explanation](https://storeleads.app/blog/2020/03/27/platform-wins-and-losses).

The longer-term counts came from [BuiltWith’s Magento statistics](https://trends.builtwith.com/shop/Magento), another automated technology-detection provider.

## How reliable is it?

| Claim | Reliability |
|---|---|
| Magento’s overall domain footprint is declining | **Moderate to reasonably strong** |
| Shopify is a major destination for former Magento domains | **Moderate** |
| Exactly 455 merchants migrated in 90 days | **Low to moderate** |
| A particular company completely migrated its commerce operation | **Low without manual verification** |
| Adobe Commerce customer or revenue churn | **Not measurable from this data** |

There are several important failure modes:

- **Domain versus merchant:** One merchant can operate many country, brand, outlet, or campaign domains. The dataset may count each separately.
- **Hybrid architectures:** A site might use Shopify for one storefront and Magento for another, or Magento as a backend behind a custom/headless frontend.
- **Temporary detection:** Deployments, redirects, maintenance pages, CDN changes, and bot protection can hide or expose technology signatures.
- **Platform remnants:** Magento scripts or URLs can remain after migration; Shopify elements can be embedded without Shopify powering the entire store.
- **Corporate-domain confusion:** A brand’s main domain may not be the domain where checkout or its principal commerce backend operates.
- **No published error rate:** Store Leads does not provide an independently audited accuracy rate or confidence interval for these migration classifications.
- **Magento versus Adobe Commerce:** External crawlers often cannot reliably determine whether an installation is Magento Open Source or licensed Adobe Commerce.

A warning sign is that the providers disagree even on the current footprint: Store Leads detects approximately **106,000 live stores**, while BuiltWith detects approximately **129,000 live Magento websites**. Their definitions and crawling systems clearly differ.

Therefore, the careful formulation is:

> Store Leads detected 455 domains changing from Magento signatures to Shopify signatures during the measured 90-day period.

It is **not** safe to say:

> 455 Magento customers definitively migrated their businesses to Shopify.

For strategic analysis, this data should be used as a **directional trend indicator**, with a representative sample of domains validated manually. It should not be presented as Adobe Commerce’s actual acquisition or churn rate. Adobe itself does not publish sufficiently detailed merchant additions, departures, or replatforming figures to verify it.
