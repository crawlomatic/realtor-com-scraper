# Realtor.com Property Scraper & Real Estate Listings API

[![Apify Store](https://img.shields.io/badge/Apify%20Store-View%20Actor-brightgreen?logo=apify)](https://apify.com/misterkhan/realtor-scraper)
[![GitHub stars](https://img.shields.io/github/stars/crawlomatic/realtor-com-scraper?style=social)](https://github.com/crawlomatic/realtor-com-scraper)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Python SDK](https://img.shields.io/badge/SDK-Python-3776AB?logo=python&logoColor=white)](https://github.com/apify/apify-client-python)
[![Node.js SDK](https://img.shields.io/badge/SDK-Node.js-339933?logo=node.js&logoColor=white)](https://github.com/apify/apify-client-js)

> Extract for-sale and rental home listings, property taxes, school ratings, and agent details from Realtor.com.

---

## ⚡ Quick Start

You can run this scraper directly via the **[Apify Store Web Console](https://apify.com/misterkhan/realtor-scraper)** with zero setup, or integrate it into your Python / Node.js backend using the code below.

### 🐍 Python Quickstart

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

# Initialize the ApifyClient with your API token
# Get your token from https://console.apify.com/account/integrations
client = ApifyClient("YOUR_APIFY_TOKEN")

# Configure input parameters
run_input = {
  "startUrls": [
    {
      "url": "https://www.realtor.com/realestateandhomes-search/Miami_FL"
    }
  ],
  "maxItems": 40
}

print("🚀 Launching Realtor.com Property Scraper & Real Estate Listings API on Crawlomatic Engine...")
run = client.actor("misterkhan/realtor-scraper").call(run_input=run_input)

# Fetch results from the Actor's default dataset
dataset_items = client.dataset(run["defaultDatasetId"]).list_items().items
print(f"✅ Successfully fetched {len(dataset_items)} records!")

for item in dataset_items[:3]:
    print(item)
```

---

### 🟢 Node.js / JavaScript Quickstart

```bash
npm install apify-client
```

```javascript
import { ApifyClient } from 'apify-client';

// Initialize the ApifyClient with your API token
const client = new ApifyClient({
    token: 'YOUR_APIFY_TOKEN',
});

// Configure input parameters
const input = {
  "startUrls": [
    {
      "url": "https://www.realtor.com/realestateandhomes-search/Miami_FL"
    }
  ],
  "maxItems": 40
};

console.log('🚀 Launching Realtor.com Property Scraper & Real Estate Listings API...');
const run = await client.actor('misterkhan/realtor-scraper').call(input);

// Fetch results
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(`✅ Extracted ${items.length} records!`);
console.dir(items.slice(0, 3));
```

---

## What does Realtor.com & Realtor.ca Property Scraper do?

Realtor.com & Realtor.ca Property Scraper is a North American residential real estate extraction tool that scrapes **homes for sale, properties for rent, and recently sold MLS listings** across both **Realtor.com (United States)** and **Realtor.ca (Canada)** in a single unified Actor.

Whether you are sourcing undervalued residential deals across US ZIP codes and Canadian postal codes, building comparative market analysis (CMA) models, or generating targeted lists of active listing agents and brokerages, this scraper delivers clean, structured property records in seconds.

> 🛡️ **Zero Proxy Configuration Required:** Anti-blocking and regional routing are **handled automatically out of the box** — just paste your target URLs and click **Start**.

## What data can you extract with Realtor.com & Realtor.ca Property Scraper?

**💵 List Price & Listing Status** — formatted `price`, numeric `list_price`, `status` (`for_sale`, `for_rent`, sold), and `property_type` (`single_family`, condo, townhome, `multi_family`, land) <br>
**🏠 Interior & Lot Dimensions** — `beds` count, `baths` count, interior living area (`sqft`), and total `lot_sqft` <br>
**📍 Full Street Address & Geocoordinates** — complete `address` (street, city, state/province, ZIP/postal code) and map coordinates <br>
**👔 Listing Agent & Brokerage Attribution** — `agent_name` and brokerage office representing the property <br>
**🖼️ Media & Direct Property Links** — unique MLS/Realtor property `id` and canonical property detail `url` <br>

## Why scrape property listings from Realtor.com and Realtor.ca?

**💪 Unified US and Canadian MLS market coverage** — query both realtor.com and realtor.ca search pages with a single scraper and schema <br>
**🕵️ Source off-radar investment properties and price drops** — filter by price per square foot, lot size, and multi-family zoning across dozens of target markets simultaneously <br>
**✨ Build active listing agent and brokerage directories** — capture `agent_name` and brokerage directly from live listings to power real estate SaaS, mortgage, staging, or solar outreach <br>
**👍 Zero proxy or account setup** — built-in anti-blocking and residential proxy routing work out of the box <br>
**📩 Automate daily new-listing alerts** — connect recurring runs to Google Sheets, Airtable, Make, or n8n to notify your acquisition team as soon as matching homes hit the market <br>

## How do I use Realtor.com & Realtor.ca Property Scraper?

Realtor.com & Realtor.ca Property Scraper is designed for fast, zero-configuration operation in Apify Console:

1. Click **Try for free** on the Actor page to open Apify Console.
2. Paste one or more Realtor.com or Realtor.ca search URLs into **Start URLs** (for example, `https://www.realtor.com/realestateandhomes-search/Austin_TX`).
3. Set **Max Results** (`maxItems`) to control how many property listings to collect.
4. Click **Start** to launch the extraction run.
5. Download your real estate dataset from the **Dataset** tab in Excel, CSV, JSON, or HTML table format.

## Input

Realtor.com & Realtor.ca Property Scraper accepts a simple 2-parameter JSON configuration. Click on the [Input tab](https://apify.com/misterkhan/realtor-scraper/input-schema) for the interactive form.

```json
{
  "startUrls": [
    {
      "url": "https://www.realtor.com/realestateandhomes-search/Austin_TX"
    }
  ],
  "maxItems": 40
}
```

**📍 `location`** — search location by US city, state, or ZIP code (e.g. `Austin, TX`, `Miami, FL`, `90210`). When provided, `startUrls` is optional <br>
**🏡 `startUrls`** — array of Realtor.com or Realtor.ca city, ZIP/postal code, neighborhood, or filtered search URLs (e.g., `https://www.realtor.com/realestateandhomes-search/Austin_TX`) <br>
**🔢 `maxItems`** — maximum number of property listings to collect per run (default: 40; Free plan runs collect up to 40 listings per run, while paid Apify plans support unlimited bulk runs) <br>

## Output sample

Results are streamed in real time to your default Apify Dataset. Each record represents a normalized residential listing with price, dimensions, address, and listing agent attribution:

```json
[
  {
    "id": "M9182736450",
    "address": "2408 Barton Hills Dr, Austin, TX 78704",
    "price": "$895,000",
    "list_price": 895000,
    "status": "for_sale",
    "property_type": "single_family",
    "beds": 4,
    "baths": 3.0,
    "sqft": 2480,
    "lot_sqft": 7405,
    "agent_name": "Sarah Jenkins",
    "brokerage": "Compass RE Texas",
    "url": "https://www.realtor.com/realestateandhomes-detail/2408-Barton-Hills-Dr_Austin_TX_78704_M91827-36450"
  }
]
```

## How much does it cost to scrape Realtor.com and Realtor.ca listings?

Realtor.com & Realtor.ca Property Scraper uses **Pay-Per-Event (PPE)** pricing (apify-default-dataset-item) with a `$0.00` startup fee—you only pay for property listings delivered to your dataset:

**🆓 Free plan** — `$0.005` per listing ($5.00 / 1,000 listings, up to 40 listings/run) <br>
**🥉 Starter (Bronze) plan** — `$0.00125` per listing ($1.25 / 1,000 listings) <br>
**🥈 Scale (Silver) plan** — `$0.0009` per listing ($0.90 / 1,000 listings) <br>
**🥇 Business+ (Gold) plan** — `$0.00065` per listing ($0.65 / 1,000 listings) <br>

With the monthly free credit on the Apify Free plan, you can extract **up to 1,000 property listings per month for free**.

> 💡 **Predictable, All-Inclusive Pay-Per-Event Pricing:** There is a **`$0.00` run start fee** and **no separate proxy configuration required**. You only pay the flat per-result rate above for data successfully delivered to your dataset — works out of the box on both **Free** and **Paid** Apify plans.

## How many results can you scrape with Realtor.com & Realtor.ca Property Scraper?

Realtor.com & Realtor.ca Property Scraper can extract **thousands of property listings per run** on paid Apify plans (up to 40 listings per run on the Free plan). Keep these best practices in mind when scraping large metropolitan areas:

- **Partition large metro searches by ZIP code or price band** — major metro areas (such as Los Angeles, Houston, Toronto, or Vancouver) have tens of thousands of active listings. Splitting your `startUrls` by individual ZIP/postal codes or price brackets ensures complete coverage across deep pagination.
- **Filter directly in the Realtor search URL** — apply any bedroom, bathroom, price, property type (single-family-home, condo), or status (/apartments/, /sold/) filter on Realtor.com or Realtor.ca in your browser, then copy and paste that filtered URL into `startUrls`.
- **Want Zestimates and Rent Zestimates too?** — pair your Realtor MLS data with our [Zillow Property Search Scraper](https://apify.com/misterkhan/zillow-scraper) to cross-reference list prices against automated valuation estimates.

## Want to scrape Zillow, ForSaleByOwner.com, or Local Real Estate Brokerages?

Combine Realtor.com & Realtor.ca Property Scraper with our published US real estate and lead enrichment Actors:

🏡 **[Zillow Search Scraper](https://apify.com/misterkhan/zillow-scraper)** — extract US homes for sale, rentals, sold prices, Zestimates, beds/baths, and coordinates (From $0.90 / 1K) <br>
🇺🇸 **[ForSaleByOwner.com US FSBO Scraper](https://apify.com/misterkhan/forsalebyowner-us-scraper)** — scrape direct commission-free US homeowner property listings and seller details (From $0.75 / 1K) <br>
📍 **[Google Maps Places Scraper](https://apify.com/misterkhan/google-maps-scraper)** — extract local brokerages, property managers, commercial businesses, phones, websites, and ratings (From $0.55 / 1K) <br>
📧 **[Website Contact & Email Scraper](https://apify.com/misterkhan/contact-enricher-scraper)** — crawl brokerage and company domains for verified business emails, phone numbers, and social links (From $0.60 / 1K) <br>
## Integrations and Realtor.com & Realtor.ca Property Scraper

Realtor.com & Realtor.ca Property Scraper connects directly with your real estate CRM, spreadsheets, and data warehouses through [Apify integrations](https://apify.com/integrations):

- **No-Code Automation** — trigger new-listing deal alerts and CRM enrichment workflows via Make, Zapier, n8n, or Clay.
- **Spreadsheets & Databases** — sync property feeds automatically to Google Sheets, Airtable, HubSpot, BigQuery, Snowflake, or PostgreSQL.
- **Webhooks** — push newly scraped properties to your underwriting model via HTTP webhook the moment a run completes.

## Using Realtor.com & Realtor.ca Property Scraper with the Apify API

You can launch property search runs and stream dataset items programmatically using the official `apify-client` libraries for **Node.js** and **Python**, or connect this Actor directly to AI real estate analysts via the **Apify MCP Server** (`https://mcp.apify.com`).

Check the [API tab](https://apify.com/misterkhan/realtor-scraper/api) for ready-to-copy Node.js, Python, and cURL code snippets.

## Frequently asked questions about Realtor.com & Realtor.ca Property Scraper

**🌎 Can I mix US (realtor.com) and Canadian (realtor.ca) URLs in the same run? <br>**
Yes. You can pass both realtor.com and realtor.ca search URLs in the `startUrls` array and the scraper will normalize both into the same output dataset schema.

**🏠 Does the scraper support rentals and recently sold homes as well as homes for sale? <br>**
Yes. Pass any Realtor for-sale (/realestateandhomes-search/...), rental (/apartments/...), or recently sold (/sold/) search URL and the `status` field will reflect the listing type automatically.

**🛡️ Do I need to configure proxies? <br>**
**No — everything works out of the box with zero setup.** Regional routing, session management, and anti-blocking are handled automatically so you do not need to configure custom proxy settings.

## Is it legal to scrape public property listings from Realtor.com and Realtor.ca?

Our scrapers are ethical and only extract publicly available real estate listing facts (asking prices, property dimensions, addresses, and public listing brokerage attributions) displayed to visitors on public property portals. For more details on the legality of web scraping, read Apify's guide on [is web scraping legal](https://blog.apify.com/is-web-scraping-legal/).

## Your feedback

We keep this Actor under active maintenance. If a run finishes successfully but returns fewer results than you expected, hangs, or errors — please **open an Issue before posting a public review** so we can diagnose and fix it for you.

**🛠️ How to report** — Use the Actor’s [Issues tab](https://apify.com/misterkhan/realtor-scraper/issues/open) in Apify Console. Include the run ID, your input JSON, and what you expected vs. what you got. <br>
**⏱️ Response time** — We aim to reply within 24 hours on business days. <br>
**⭐ Reviews** — Happy with the results? A short positive review helps other users find a reliable scraper. Ran into a problem? Open an Issue first — we’ll work with you to resolve it before you leave a rating. <br>


---

## 🛡️ Architecture & Engine Reliability

This scraper runs on the **[Crawlomatic Engine](https://crawlomatic.com)**:
- **Zero Proxy Configuration:** Intelligent residential and datacenter proxy rotation with automated regional ccTLD binding.
- **WAF Bypass Engine:** Autonomous challenge solving for Cloudflare Turnstile, DataDome, PerimeterX, Kasada, and Akamai.
- **Pay-Per-Event (PPE) Pricing:** Transparent pay-as-you-go pricing with \$0 starting fee.

## 📄 License

Apache License 2.0. See [LICENSE](LICENSE) for details.

Developed & Maintained by **[Crawlomatic](https://crawlomatic.com)**.
