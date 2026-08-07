# Public subscriber and deployment data for AWS Marketplace software

After searching AWS Marketplace product pages, AWS documentation, Marketplace APIs, seller reports, dashboards, public datasets, third-party services, and vendor disclosures, the conclusion is:

> AWS does not appear to publish numeric subscriber, deployment, VM, or usage totals for individual AWS Marketplace software products.

The nearest public information is a **relative monthly popularity ranking**, not actual totals.

## What is publicly available

### “Most subscribed products last month”

The [AWS Marketplace homepage](https://aws.amazon.com/marketplace/) publishes ranked lists such as:

- Most subscribed SaaS products
- Most subscribed AMI products
- Most subscribed container products
- Most subscribed machine-learning products
- Most subscribed free products

Products are displayed as “Top 1,” “Top 2,” and so forth. AWS does not disclose whether the first product received ten, one hundred, or ten thousand subscriptions.

This is the strongest first-party public adoption signal found.

Important limitations:

- It measures subscriptions during the previous month, not total active subscribers.
- Separate delivery categories have separate rankings.
- Free and paid products may be ranked separately.
- AWS does not publish the calculation methodology.
- Private offers and renewals may affect the ranking differently from public purchases.
- A subscription does not necessarily mean that the software was deployed or actively used.

### Product reviews

Product pages expose AWS reviews and sometimes imported external reviews. These are weak adoption proxies:

- Most buyers do not leave reviews.
- External reviews may cover customers acquired outside AWS Marketplace.
- Review counts cannot reliably be converted into subscriber totals.

### Marketplace-wide totals

AWS publicly advertises approximately:

- **25,000+ products**
- **6,000+ sellers**
- More than 70 categories

These are catalog-supply figures, not subscriber or deployment totals. See the [AWS Marketplace overview](https://aws.amazon.com/marketplace/features/what-is-aws-marketplace).

## What AWS tracks but keeps private

AWS clearly possesses the requested data. It exposes it only to the relevant seller, buyer, reseller, or AWS account.

### Seller subscriber reports

AWS provides sellers with customer subscriber reports containing:

- Product ID
- Subscriber AWS account ID
- Subscription date
- Offer information
- Whether a subscription is active
- New and cancelled subscriptions

The report is private to the seller and available through the AWS Marketplace Management Portal or Commerce Analytics Service. AWS documentation describes it as a list of customers subscribed to the seller’s products.

Therefore, a seller can calculate the number of subscribers to **its own products**, but cannot obtain corresponding figures for competitors.

### Seller usage dashboard

The private [AWS Marketplace Usage dashboard](https://docs.aws.amazon.com/marketplace/latest/userguide/usage-dashboard.html) contains approximately the requested information:

- Customer consumption
- Product and offer
- Subscriber and payer
- Usage dimensions
- AMI instance types
- Usage amounts
- Agreement start dates
- Six months of rolling usage data

It requires authentication to the seller account. It is not visible on the public product page.

### Agreements and renewals dashboard

AWS also has a private [Agreements and renewals dashboard](https://docs.aws.amazon.com/marketplace/latest/userguide/agreements-renewals-dashboard.html), which includes subscriber account IDs, products, offers, and agreement status. Again, access is limited to the parties involved.

### Buyer subscription view

A buyer can view subscriptions owned by its own AWS account or organization. It cannot view subscriptions belonging to other AWS customers.

## Why “number of VMs” is especially difficult

AWS Marketplace supports several fulfillment models:

- AMI/EC2
- Containers and Helm charts
- SaaS
- CloudFormation-based products
- Machine-learning models
- Professional services
- Data products

There is no common concept equivalent to an installed application.

For an AMI product:

1. An AWS account subscribes to the product.
2. It may launch zero, one, or hundreds of EC2 instances.
3. Instances can be short-lived or persistent.
4. The customer can create derivative AMIs that retain the Marketplace product code.
5. Autoscaling can change the active count continuously.
6. Some products meter hours, hosts, users, requests, or custom consumption dimensions rather than VM count.

AWS attaches a product code to Marketplace AMIs so that usage can be metered and billed, as described in its [AMI product documentation](https://docs.aws.amazon.com/marketplace/latest/userguide/ami-getting-started.html). However, the resulting instance and billing data is private.

Consequently:

- Subscriber accounts ≠ deployments
- Deployments ≠ running VMs
- Running VMs ≠ active users
- Usage units may not correspond to any of those measures

## Do AWS APIs expose it?

No adoption-count field was found in the public catalog or discovery interfaces.

The current [AWS Marketplace Discovery API](https://docs.aws.amazon.com/marketplace/latest/developerguide/discovery-apis.html) exposes:

- Listings
- Products
- Categories
- Reviews
- Sellers
- Fulfillment options
- Offers and pricing
- Legal and commercial terms

Its documented data model does not include subscriber counts, deployed instances, revenue, or consumption.

Furthermore, access requires AWS credentials and, according to AWS onboarding documentation, seller or reseller eligibility. Even with access, it is a product-discovery interface, not a competitor-sales-data API.

The older Marketplace Catalog API is similarly oriented toward sellers managing their own products, offers, and private marketplaces. It does not provide competitor subscription figures.

## Third-party sources

No credible equivalent of BuiltWith or Store Leads was found for AWS Marketplace installations.

That absence makes sense:

- SaaS subscriptions are not externally observable.
- EC2 instances are inside private AWS accounts.
- Marketplace AMIs do not necessarily expose identifiable public web signatures.
- Private offers conceal transaction prices.
- Enterprise deployments often have no public endpoint.
- AWS account and billing information is confidential.

Some third-party cloud-marketplace companies track listing metadata, pricing, and seller activity, but none were found publishing defensible per-product subscriber or VM totals.

Vendor press releases occasionally provide figures such as:

- Total company customers
- AWS Marketplace transaction value
- Marketplace revenue growth
- Number of enterprise deals

For example, AWS and Snowflake reported more than $2 billion in annual AWS Marketplace sales, while also mentioning Snowflake’s 12,600 total global customers. Those two figures do **not** establish how many Snowflake customers subscribed through AWS Marketplace. See the [AWS/Snowflake announcement](https://press.aboutamazon.com/aws/2025/12/snowflake-doubles-aws-marketplace-growth-yoy-eclipses-2-billion-in-sales-as-new-integrations-accelerate-enterprise-data-and-ai-adoption).

## Available measures and confidence

| Measure | Public? | Usefulness |
|---|---:|---|
| Monthly “most subscribed” rank | Yes | Best relative adoption signal |
| Numeric total subscribers per product | No | Seller-only |
| New/cancelled subscribers | No | Seller-only |
| Active agreements | No | Seller/party-only |
| Product VM or instance hours | No | Seller-only usage reporting |
| Current running VM count | No | Private customer infrastructure |
| Revenue or GMV per product | Generally no | Occasional voluntary disclosure |
| Reviews | Yes | Very weak proxy |
| Listing age and update history | Partly | Activity proxy, not adoption |
| Pricing and fulfillment type | Yes | Descriptive only |
| Vendor-reported total customers | Sometimes | Usually not Marketplace-specific |

## Bottom line

There is a public AWS page that tells you **which products had the most new subscriptions relative to others during the previous month**. No public page or API was found that reveals:

- The numeric subscriber total for a product
- Total historical subscriptions
- Active subscribers
- Number of Marketplace deployments
- Running VM counts
- Instance hours
- Product-specific revenue

Exact data exists in AWS seller reports and dashboards, but each seller can see only its own performance. For competitive research, the best public approach would be to archive AWS’s monthly rankings and combine them with listing age, reviews, pricing, vendor disclosures, and detectable public deployments. That can produce a relative popularity index, but not a defensible subscriber or VM estimate.
