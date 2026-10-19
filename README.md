# Toll Brothers New Homes Scraper [💰$1.35]

Extract structured data from [Toll Brothers new](https://tollbrothers.com) — Toll Brothers new-construction home designs by state or community: model name, starting price, beds, baths and square-foot ranges, community, address, coordinates, sales phone, photos and optional floorplans. Structured JSON, ready for market research.

**[Toll Brothers New Homes Scraper [💰$1.35] on Apify →](https://apify.com/blackfalcondata/tollbrothers-com-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by description format, and more.

**Detail enrichment** — Fetch full descriptions, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from Toll Brothers new on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from Toll Brothers new.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Lead generation**
Extract contact details alongside ${NOUNS} to build targeted outreach lists for sales teams, partnerships, or B2B prospecting.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "Scottsdale",
  "location": "Arizona",
  "maxResults": 100,
  "includeDetails": true,
  "descriptionMaxLength": 0,
  "compact": false,
  "descriptionFormat": "all",
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Filter by home design, community, city or home type (e.g. Scottsdale, Villas). Leave empty to get every home design. |
| `location` | string | — | US state to search, e.g. Arizona or AZ. Leave empty to cover every state Toll Brothers builds in. |
| `maxResults` | integer | `100` | Maximum total results (0 = unlimited). |
| `startUrls` | array | `[]` | Paste raw search URLs from the target site. Each URL becomes its own search task; results are merged and deduped by listing ID across all URLs. When provided, startUrls REPLACE the query/location fields (each supported URL becomes one task; unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `includeDetails` | boolean | `true` | Fetch full listing details. |
| `descriptionMaxLength` | integer | `0` | Truncate description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `descriptionFormat` | enum | `"all"` | Pick a single description representation. `all` keeps every variant; `text` / `html` / `markdown` drop the others. |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (queries, locations, startUrls, country) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `emitUnchanged` | boolean | `false` | In incremental mode, also emit records that haven't changed since last run. |
| `emitExpired` | boolean | `false` | In incremental mode, also emit records no longer found on Toll Brothers. |
| `skipReposts` | boolean | `false` | When incremental, skip listings whose content matches an expired listing from a prior run (cross-run duplicate detection). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED listings. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of listings included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `lat` | number | — | GPS latitude. Pair with lon. |
| `lon` | number | — | GPS longitude. Pair with lat. |
| `radiusKm` | integer | — | Search radius in kilometres around the given coordinates. |

---

## Output fields

Every listing returns the same 54-field schema. Missing values are `null` — never omitted.

- `url`
- `name`
- `title`
- `communityName`
- `communityUrl`
- `collectionName`
- `communityId`
- `homeType`
- `state`
- `city`
- `county`
- `zip`
- `metroName`
- `cpRegion`
- `description`
- `badgeText`
- `pricedFrom`
- `pricedFromValue`
- `communityPricedFrom`
- `lowestMatchingPrice`
- `isMinPrice`
- `isMaster`
- `isFuture`
- `partOfMaster`
- `hasQdh`
- `hasExternalDomain`
- `lat`
- `lon`
- `phone`
- `oscPhone`
- `headerTitle`
- `homeTypes`
- `communityTypes`
- `homeProperties`
- `qdhCount`
- `modelCount`
- `highriseCount`
- `options`
- `imageUrl`
- `imageGallery`
- `community`
- `home`
- `homeDetail`
- `scrapedAt`
- `portalUrl`
- `distanceKm`
- `location`
- `listingId`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "url": "https://www.tollbrothers.com/luxury-homes-for-sale/Arizona/Sereno-Canyon/Estate-Collection/Sunburst",
  "name": "Sunburst",
  "title": "Sereno Canyon - Estate Collection is an award-winning community in an amenity-rich master plan featuring new luxury estate homes in Scottsdale, AZ, on spectacular desert- and mount…",
  "communityName": "Sereno Canyon - Estate Collection",
  "communityUrl": "https://www.tollbrothers.com/luxury-homes-for-sale/Arizona/Sereno-Canyon/Estate-Collection",
  "collectionName": "Estate Collection",
  "communityId": 13192,
  "homeType": "Single-Family Home",
  "state": "AZ",
  "city": "Scottsdale",
  "county": "Maricopa",
  "zip": "85255"
}
```

*Truncated — full records contain 54 fields. See Output fields for the complete schema.*

**[Try Toll Brothers New Homes Scraper [💰$1.35] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/tollbrothers-com-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.0063 |
| Result | $0.00135 |

See the [actor on Apify](https://apify.com/blackfalcondata/tollbrothers-com-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape Toll Brothers new?**
Use this actor on Apify to extract structured data from tollbrothers.com. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get Toll Brothers new data as JSON, CSV, or Excel?**
The actor writes each listing to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape Toll Brothers new?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check Toll Brothers new's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage. Expired listings can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Toll Brothers New Homes Scraper [💰$1.35]](https://apify.com/blackfalcondata/tollbrothers-com-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
