# Webshop and commerce solutions in AWS Marketplace

Research date: **August 7, 2026**.

## Scope and reading notes

This is a best-effort inventory of distinct webshop or commerce **platform families** offered through the public AWS Marketplace catalog. It includes products that provide a catalog, cart/checkout, order entry, or marketplace storefront. It does not count every reseller AMI for the same open-source platform as a separate competitor.

The inventory contains **24 identifiable solution families/offers**:

- 16 direct commerce platforms: seven enterprise/SaaS products and nine self-hosted platforms.
- Four specialist or service-led commerce offers.
- Four broader business or digital-experience suites with a webshop module.

This is platform-family coverage, not a guarantee that every regional, private, discontinued, or newly published Marketplace SKU is represented. AWS Marketplace search is dynamic, and some products are visible only to signed-in buyers or in specific countries.

AWS Marketplace does **not** disclose subscriptions, active deployments, or running VM counts for individual products. Consequently, the “public adoption signal” below uses the strongest attributable metric found: vendor-reported customers/stores/transaction volume or AWS Marketplace rating counts. These metrics are not directly comparable and must not be read as Marketplace sales.

Pricing also needs care:

- AMI prices are the **seller's software/support charge only**. EC2, EBS, data transfer, database, CDN, backup, and operations remain additional. Approximate monthly figures use 730 hours.
- Enterprise SaaS listings commonly use private offers. Several pages display nominal metering dimensions that are clearly not usable estimates of real contract value; those are labeled as such.
- AWS documents the available Marketplace models—including free, BYOL, hourly, usage, and contract pricing—and confirms that AMIs always incur separate infrastructure charges ([AWS pricing overview](https://docs.aws.amazon.com/marketplace/latest/userguide/pricing-overview.html), [AMI pricing](https://docs.aws.amazon.com/marketplace/latest/userguide/pricing-ami-products.html)).

## Direct enterprise and SaaS commerce platforms

| Platform and AWS offer | Delivery | Public adoption signal | Public AWS Marketplace price | Short feature list |
|---|---|---|---|---|
| [commercetools](https://aws.amazon.com/marketplace/pp/prodview-msebsxnshhblk) | SaaS, deployed on AWS | Vendor says **450+ companies**; **29 ratings** (5 AWS, 24 external) | **$50,000 / 12 months** for the displayed Standard entitlement; appropriately sized contracts require vendor confirmation | Composable, cloud-native, API-first/headless; B2C and B2B; business units, quotes, roles, customer pricing and discounts; versionless upgrades |
| [Spryker Cloud Commerce OS](https://aws.amazon.com/marketplace/pp/prodview-jxoozx4bi2x56) | SaaS, deployed on AWS | Vendor says **150+ enterprise customers**; **146 ratings** (6 AWS, 140 external) | Listing displays **$900,000 / 12 months**, while describing variable licensing and directing buyers to the vendor; treat as a reference dimension/private-offer starting point | Headless and API-first; B2B, B2C and D2C; enterprise marketplaces; “Thing Commerce”; modular application composition and integrations |
| [Elastic Path Commerce Cloud](https://aws.amazon.com/marketplace/pp/prodview-chxlfw7pkmfts) | SaaS, deployed on AWS; free trial | Seller profile says **250+ leading enterprises**; **26 ratings** | **Private/contract pricing**; no usable public amount | MACH/headless commerce; Product Experience Manager; storefront and landing-page builder; Composer integration layer; payments; self-managed commerce components |
| [HCL Commerce Cloud](https://aws.amazon.com/marketplace/pp/prodview-rz2dybrf7jbyc) | SaaS, deployed on AWS | Vendor says it processes **more than $220B in commerce transactions per year**; **7 ratings** | **Private offer only**. The page may show **$350,000 / 12 months**, but explicitly says the listing is informational and grants no access without an HCL private offer | B2B, B2C, B2B2C and D2C; intelligent search; headless starter store; marketplace; merchandising; contract pricing/workflows; real-time inventory; post-order service |
| [VTEX Commerce Suite Enterprise](https://aws.amazon.com/marketplace/pp/prodview-kml5odmpw2pww) | SaaS, deployed on AWS | Customers operate in **32 countries**; **37 ratings** on the global listing | **Private offer**. The public page's $1M recurring dimension is a procurement placeholder, not a defensible monthly quote | Integrated ecommerce, marketplace and order-management system; microservice architecture; catalog, promotions, logistics and omnichannel fulfillment; developer and business tools |
| [Commerce Layer](https://aws.amazon.com/marketplace/pp/prodview-a7l6raugrltqm) | SaaS | No total disclosed; listing names **14 customer brands**; **0 ratings** | Page displays **$1,000 per placed order**. This is commercially anomalous and should be confirmed with the vendor before comparison | API-first/headless engine; production micro-frontends; subscriptions, POS and multi-vendor models; local payments/currency; 400+ API endpoints, 100+ webhook events; stated 99.99% uptime |
| [Agiliron Premier Edition](https://aws.amazon.com/marketplace/pp/prodview-va6ty7ravmp7i) | SaaS; listing says not deployed on AWS | **29 ratings**; no customer total disclosed | **$99/month** base for 1 user and 2 sales channels; **+$49/user/month**, **+$49/channel/month**, **+$24/POS lane/month** | B2C and B2B webstores; POS; Amazon/eBay and EDI; synchronized products, inventory and orders; CRM/ERP/back office; warehouse management; PCI Level 1 |

### Enterprise interpretation

The closest Magento/Adobe Commerce substitutes are **commercetools, Spryker, Elastic Path, HCL Commerce Cloud, and VTEX**. They address complex multi-brand, multi-market, B2B/B2C, and omnichannel programs, but nearly all require a negotiated license and implementation project. Commerce Layer is a narrower API-first engine. Agiliron is a lower-cost all-in-one option aimed at smaller multichannel operators.

## Self-hosted webshop platforms sold as AMIs

These are the most IaaS-like competitors: the buyer launches and operates the platform in their own AWS account. Multiple sellers often repackage the same open-source code. The table uses one current representative listing per platform so seller packaging is not mistaken for product diversity.

| Platform and representative AWS offer | Seller / delivery | Public adoption signal | Seller charge in AWS Marketplace | Short feature list |
|---|---|---|---|---|
| [Magento Open Source, Bitnami package](https://aws.amazon.com/marketplace/pp/prodview-zthfwp2zvh2fq) | Bitnami by VMware / AMI | AWS exposes no installations; Adobe refers only to [**“millions of people”**](https://business.adobe.com/products/commerce/magento/open-source.html) in the Magento community, not a current store count | **$0 software fee**, plus AWS infrastructure | Multi-storefront catalog and checkout; extensible PHP platform; CRM, ERP, payment and shipping extensions; MariaDB-based stack |
| [WooCommerce on AWS](https://aws.amazon.com/marketplace/pp/prodview-mrm6fiuolib44) | Webkul / AMI; 7-day trial | Woo reports **4.1M+ live installations** and **30.5% of ecommerce**, based on StoreLeads July 2026; AWS listing has **0 ratings** ([Woo source](https://woocommerce.com/newsroom/)) | **$0.02/hour** (about **$14.60/month**) plus AWS | WordPress-based storefront; catalog and inventory; themes/plugins; payment gateways; shipping and tax; HTTPS |
| [OpenCart](https://aws.amazon.com/marketplace/pp/prodview-aaphca5msbp6e) | TurnKey Linux / AMI; 30-day trial | No current attributable store/user count found; AWS listing has **0 ratings** | **$0.02/hour** (about **$14.60/month**) plus AWS | Multi-store administration; product/catalog and order management; themes/extensions; automated security updates; one-click backup, restore and migration |
| [PrestaShop 9](https://aws.amazon.com/marketplace/pp/prodview-2xuapz7a7fixq) | cloudimg / AMI; 7-day trial | Listing says PrestaShop is trusted by **300,000+ merchants**; **0 ratings** | Recommended m5.large: **$0.08/hour** (about **$58.40/month**); micro instances **$0.04/hour**; plus AWS | Catalog, cart and checkout; modules/themes; Apache/PHP/MariaDB; separate EBS web/database volumes; unique credentials and vendor support |
| [Shopware 6](https://aws.amazon.com/marketplace/pp/prodview-or5ais6ofksvg) | ATH Infosystems / AMI; 5-day trial | Shopware reports **100,000+ businesses**; listing has **0 ratings** ([Shopware source](https://www.shopware.com/en/news/shopware-examples/)) | Recommended m4.large: **$0.10/hour** (about **$73/month**); t2.micro **$0.001/hour**; plus AWS | API-first and headless; B2C and B2B; multi-store/multi-region; content/storytelling CMS; workflows, plugins, and full data ownership |
| [Saleor](https://aws.amazon.com/marketplace/pp/prodview-6avjryazihnmg) | Waltsoft / AMI; 5-day trial | No customer total; listing claims capacity for **10K+ concurrent shoppers** and **50+ storefronts**; **0 ratings** | Recommended t3.medium: **$0.01/hour** (about **$7.30/month**); t3.micro **$0**; plus AWS | GraphQL-first headless platform; multichannel catalog; warehouses; Docker deployment; RBAC and SSO/OIDC |
| [Sylius](https://aws.amazon.com/marketplace/pp/prodview-ngokj2fh5u6m6) | Waltsoft / AMI; 5-day trial | No customer total; listing claims **200+ attributes/variants**, **5+ storefronts**, and **100+ extensions**; **0 ratings** | Recommended t3.medium: **$0.01/hour** (about **$7.30/month**); t3.micro **$0**; plus AWS | Symfony/PHP framework; headless REST API; multichannel catalogs; products, promotions, checkout, orders and extensibility |
| [Bagisto](https://aws.amazon.com/marketplace/pp/prodview-7noj4rfzjjl44) | Webkul / AMI; 5-day trial | No customer total disclosed; **0 ratings** | **$0.02/hour** (about **$14.60/month**) plus AWS. A separate Waltsoft package lists $0.01/hour on its recommended instance | Laravel-based platform; product, customer and order management; multi-channel inventory; single-seller, multivendor and B2B options |
| [Zen Cart](https://aws.amazon.com/marketplace/pp/prodview-vcvhsfiticouw) | TurnKey Linux / AMI | No customer total disclosed; **0 ratings** | **$0.02/hour** (about **$14.60/month**) plus AWS | Traditional catalog/cart/checkout; multi-language and multi-currency; extensions/templates; automatic security updates; backup/restore/migrate tools |

### Self-hosted interpretation

**WooCommerce** has by far the strongest published adoption signal in this group. **PrestaShop** and **Shopware** also publish substantial merchant/business counts. Saleor, Sylius, and Bagisto compete more on modern framework architecture and low entry cost than on publicly demonstrated AWS Marketplace traction.

The AMI sticker price is rarely the decision-driving cost. Production TCO depends more on AWS sizing, high availability, database/search services, CDN/WAF, monitoring, patching, extensions, and engineering support. A $0.01/hour image can therefore cost more to operate than a paid SaaS platform in a small team.

## Specialist and service-led commerce offers

| Offer | Delivery | Public adoption signal | Pricing | Short feature list |
|---|---|---|---|---|
| [Mirakl Platform](https://aws.amazon.com/marketplace/pp/prodview-3l7tt25a3kqja) | SaaS, deployed on AWS | **14 ratings**; vendor highlights **180+ commerce consultants**, which is an ecosystem size rather than customer count | Private/custom in practice. Public **$0.01** access, subscription, and revenue-share dimensions are nominal metering placeholders | Third-party marketplace and dropship; seller onboarding; catalog/offers; seller dashboards; promotions/ads; AI catalog mapping; headless integrations |
| [ONe B2B ecommerce platform](https://aws.amazon.com/marketplace/pp/prodview-x3ddwiiajo6g6) | Professional service; listing says not deployed on AWS | Not disclosed | **Private offer** | B2B online and offline ordering; merchant panel, e-kiosk and back office; individual commercial terms; PWA/custom frontend; ERP and finance integrations; hosting and updates |
| [OrderServ](https://aws.amazon.com/marketplace/pp/prodview-elavmsbwmwzmk) | Professional service | Not disclosed | **Private offer** | Unified ordering, payment and fulfillment across web, apps, kiosks, aggregators and stores; AI upsell/personalization; POS, KDS, loyalty and delivery integrations |
| [DIGITAL e-COMMERCE](https://aws.amazon.com/marketplace/pp/prodview-nbpilrxc4rvjw) | Professional service by T-Systems | Not disclosed | **Custom/private** | Modular purchasing, warehouse and delivery workflows; order tracking; web/mobile access; reference architecture using Elastic Beanstalk, Aurora, S3 and CloudFront |

Mirakl is primarily a marketplace operator platform rather than a conventional single-merchant shop. The other three are included because their listings promise an operational commerce system, but they are procured as service engagements rather than click-to-deploy software licenses.

## Broader suites that can run a webshop

These products are credible alternatives when a buyer wants ecommerce combined with ERP, PIM, DAM, CMS, CRM, or manufacturing rather than a standalone commerce engine.

| Platform and AWS offer | Delivery | Public adoption signal | Seller charge | Ecommerce-relevant features |
|---|---|---|---|---|
| [Odoo, Bitnami package](https://aws.amazon.com/marketplace/pp/prodview-36s27ukn6qcwc) | AMI | **15 AWS ratings**; listing cites **20,000+ contributors**, not users | **$0 software fee**, plus AWS | Website/ecommerce tied to CRM, sales, inventory, accounting and supply chain; 3,000 modules; role/access controls |
| [Pimcore, Bitnami package](https://aws.amazon.com/marketplace/pp/prodview-qxrldqviesswi) | AMI | No customer or AWS deployment count published on the listing | No public seller amount displayed; AWS infrastructure additional | Integrated ecommerce plus PIM, DAM, CMS/DXP, marketing campaigns, multichannel publishing and web-to-print |
| [ERPNext with Websoft9](https://aws.amazon.com/marketplace/pp/prodview-rtwnv5bj57i5o) | AMI; 5-day trial | **1 AWS rating**; no customer total disclosed | Recommended t3.large: **$0.055/hour** (about **$40.15/month**) plus AWS | ERP for retail/distribution with website/store capabilities; CRM, inventory, accounting and order operations; Docker; Websoft9 console and 200+ application templates |
| [Apache OFBiz Enterprise ERP](https://aws.amazon.com/marketplace/pp/prodview-7qdcetzpefziq) | AMI; 5-day trial | **0 ratings**; no customer total disclosed | Recommended t3.large: **$0.04/hour** (about **$29.20/month**) plus AWS | Ecommerce storefront and catalog/pricing; inventory; orders, returns and tax; accounting, CRM, manufacturing and CMS |

## Packaging duplicates and boundary cases

- **Websoft9** provides a general [Applications Hosting Platform](https://aws.amazon.com/marketplace/pp/prodview-5jziwpvx4puq4) with 300+ templates, including Magento, nopCommerce, Odoo, PrestaShop, Saleor and WordPress/WooCommerce. It is a deployment wrapper, not six new commerce engines. Its platform pricing is usage-based and AWS infrastructure is additional.
- **nopCommerce** was found as a deployable Websoft9 template, but no current dedicated public AWS Marketplace product page was found. It is therefore a boundary case rather than a separately priced row.
- AWS has a [Spree Commerce seller profile](https://aws.amazon.com/marketplace/seller-profile?id=df7f7798-ed77-4124-b978-be7c7130a654), but no active transactable product page was found in the public catalog during this research.
- Multiple Magento, WooCommerce, OpenCart, PrestaShop and other open-source AMIs exist from different image vendors. Counting those as distinct webshop solutions would overstate competitive variety; they mainly differ in OS image, support, bundled control panel, and seller fee.
- Magento/Adobe Commerce hosting, migration, tax, payment, fraud, search, personalization, delivery, analytics and implementation products were excluded unless the offer itself supplies a working commerce/storefront platform. That removes the managed Magento hosters listed in the previous version of this document from the primary competitive set.
- No directly transactable first-party **Shopify, BigCommerce, SAP Commerce Cloud, Salesforce Commerce Cloud, or Adobe Commerce** platform listing was found. Marketplace results for these names were integrations, consulting, migration, or hosting offers. Their absence here means “not offered as a public AWS Marketplace webshop product,” not “not a Magento competitor in the wider market.”

## Competitive takeaways for Magento

1. **Enterprise pressure is composable and managed.** commercetools, Spryker, Elastic Path, HCL, VTEX, and Commerce Layer sell API-first/headless or managed-cloud operating models. Their pitch is faster change and less platform maintenance, not a cheaper VM.
2. **Open-source pressure is inexpensive but operationally similar.** WooCommerce, Shopware, PrestaShop, OpenCart, Saleor, Sylius and Bagisto can all enter through very low seller fees, but the buyer still owns production architecture and operations—much like Magento Open Source.
3. **WooCommerce is the clearest adoption-scale threat.** Its 4.1M+ live-installation claim is materially stronger than any public Marketplace signal available for the other self-hosted offers.
4. **B2B is crowded.** Spryker, commercetools, HCL, Shopware, ONe, Agiliron and Magento all position around business accounts, contract/customer-specific pricing, approvals, quotes or multichannel sales.
5. **AWS Marketplace is primarily a procurement channel here.** The enterprise values shown on product pages should not be used for TCO comparison without private quotes, while AMI hourly charges omit most of the real operating cost.

## Data-quality legend

- **Vendor says / listing says**: self-reported by the seller; not independently verified.
- **AWS ratings**: reviews shown on the product page, not subscriptions, customers, VMs, or deployments.
- **External ratings**: syndicated by AWS from PeerSpot.
- **Not disclosed**: no defensible public count was found; it does not imply zero customers.
- **About $/month**: seller hourly fee multiplied by 730 hours; excludes every AWS infrastructure charge and tax.
