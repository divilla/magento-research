# What is headless Magento?

Headless Magento means using Magento for the **commerce backend**, while a separate application provides the customer-facing storefront.

```text
Customer
   ↓
Vue / React / Next.js storefront
   ↓ GraphQL or REST
Magento
   ├── Products
   ├── Prices
   ├── Inventory
   ├── Customers
   ├── Carts
   ├── Checkout
   └── Orders
```

Magento's traditional themes, PHP templates, layout XML, RequireJS and Knockout frontend are mostly bypassed.

## Traditional versus headless

### Traditional Magento

Magento builds the HTML page on the server:

```text
Browser → Magento controller → PHP block → .phtml template → HTML
```

Magento controls both the commerce logic and presentation.

### Headless Magento

A standalone frontend requests commerce data through APIs:

```text
Browser → Vue/React application → Magento GraphQL API → Magento services
```

The frontend renders the page and owns navigation, presentation and browser interactions. Magento remains responsible for commerce operations.

## What remains in Magento

A headless deployment typically continues using Magento for:

- Product and category management
- Attributes and variants
- Prices and promotions
- Inventory
- Customer accounts
- Carts
- Checkout
- Taxes
- Shipping and payments
- Orders, invoices and refunds
- Admin interface
- ERP and PIM integrations
- Backend custom modules

Merchants generally continue managing the store through Magento Admin.

## What moves to the frontend application

The separate application owns:

- Page rendering
- Navigation
- Product and category presentation
- Search interface
- Cart interface
- Checkout interface
- Customer-account pages
- Content presentation
- Analytics integration
- Browser-side customizations
- Performance and caching strategy

Common frontend technologies include:

- Vue and Nuxt
- React and Next.js
- PWA Studio
- Vue Storefront
- Custom mobile applications

## Example request

When a customer opens a product page:

```text
1. Next.js receives /blue-shirt.html
2. It sends a GraphQL query to Magento.
3. Magento loads the product, price and inventory.
4. Magento returns structured JSON.
5. Next.js renders the page.
```

A simplified query might look like:

```graphql
query {
  products(filter: { url_key: { eq: "blue-shirt" } }) {
    items {
      sku
      name
      description {
        html
      }
      price_range {
        minimum_price {
          final_price {
            value
            currency
          }
        }
      }
    }
  }
}
```

Magento returns data, not a complete HTML product page.

## Headless does not mean customization-free

Backend customizations remain relevant. A custom Magento module might:

- Modify product prices
- Add GraphQL fields
- Change checkout validation
- Connect orders to an ERP
- Implement special inventory rules
- Integrate a payment provider

Frontend customizations move into the Vue or React codebase.

A feature can therefore span both systems:

```text
React delivery-date component
             ↓
Custom Magento GraphQL field
             ↓
Magento validation module
             ↓
Order database
```

## Advantages

- Freedom to use a modern frontend framework
- Independent frontend deployment
- Better control over performance and user experience
- Easier support for mobile apps and multiple sales channels
- Cleaner separation between presentation and commerce logic
- Potentially easier migration away from Magento later

## Disadvantages

- Two applications must be developed and operated
- Checkout and customer authentication become more complex
- Some Magento extensions assume traditional themes
- Frontend extension compatibility is reduced
- Previewing CMS content can be harder
- GraphQL coverage may need custom modules
- Caching and data consistency require careful design

## Why it matters for migration

Headless Magento stores are strong early migration candidates because their storefront is already separated from Magento.

If the Go platform implements the GraphQL operations that an existing storefront uses:

```text
Existing React/Vue storefront
             ↓
Magento-compatible GraphQL layer
             ↓
New Go commerce platform
```

the merchant may be able to retain most of the frontend. Magento's data, commerce logic and backend customizations can be migrated while minimizing visible storefront changes.

That makes headless Magento migration more like replacing an API provider than rebuilding an entire website.
