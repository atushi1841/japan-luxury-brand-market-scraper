# Japan Luxury Brand Market — Cross-Shop Price Comparison

[![Apify Store](https://img.shields.io/badge/Apify-Store-blue)](https://apify.com/fruitful_quintessence/japan-luxury-brand-market-scraper)

**Compare used luxury brand prices (bags, wallets, jewelry, watches) across Japan's top resale retailers in a single dataset.**

Scrapes listings from **Komehyo (コメ兵)** — one of Japan's largest luxury resale chains (bags, wallets, jewelry, watches) — and **Jackroad (ジャックロード)** — Tokyo's leading pre-owned luxury watch dealer. Each item is tagged with its `source`, `shop`, and `category` so you can compare prices for the same brand across shops.

## Why this is useful

- **Cross-shop price comparison** — the same Hermès bag often differs by 5-20% between shops
- **Resale arbitrage** — find underpriced luxury items, sell at market rate
- **Price monitoring** — track market moves before buying/selling
- **Rank tracking** — compare condition ranks (中古品A/B, 未使用品) across shops

## Input

| Field | Type | Default | Description |
|---|---|---|---|
| `searchKeyword` | string | `エルメス` | Brand keyword (empty = full category scan) |
| `maxItems` | integer | 100 | Max items to collect |
| `maxPages` | integer | 2 | Max pages per source |
| `sources` | string | `komehyo,jackroad` | Comma-separated source list |

## Output fields

| Field | Description |
|---|---|
| `productId` | Product ID at source shop |
| `title` | Product title |
| `price` | Price in JPY |
| `brand` | Brand (Hermès, Louis Vuitton, Rolex...) |
| `shop` | Source shop name |
| `category` | Category (バッグ/財布・アクセサリー/ジュエリー/時計) |
| `condition` | Condition (未使用品/中古品A/B...) |
| `rank` | Komehyo condition rank |
| `referencePrice` | Reference price (上代) |
| `source` | `komehyo` or `jackroad` |
| `imageUrl` | Product image URL |
| `productUrl` | Product page URL |
| `scrapedAt` | Scrape timestamp |

## Output sample

```json
{
  "productId": "230-000-742-0039",
  "title": "【未使用品】エルメス ガーデン パーティ 30cm 051568CK バッグ",
  "brand": "HERMES",
  "price": 1100000,
  "referencePrice": 694100,
  "rank": "未使用品",
  "size": null,
  "material": null,
  "store": "名古屋本館",
  "imageUrl": "https://img.komehyo.jp/contents/images/goods/9ff/2300007420039_1_icon.jpg",
  "productUrl": "https://komehyo.jp/product/230-000-742-0039/",
  "category": "バッグ",
  "source": "komehyo",
  "shop": "Komehyo",
  "condition": "未使用品",
  "scrapedAt": "2026-08-10T09:55:15Z"
}
```

The `source` + `store` fields let you compare the same brand item across shops: run once with `searchKeyword: "エルメス"` and get Komehyo and Jackroad prices side by side.

## Pricing

Pay per event — $0.00005/run + **$0.002/item**.
## Integrations

Works with Apify [Connectors](https://apify.com/integrations) — push results to Slack, Google Sheets, Notion, Supabase, or GitHub with one click (no code needed). Trigger on a [Schedule](https://apify.com/docs/schedules) for daily price monitoring.


## Data source notes

- **Komehyo**: server-side rendered category pages (`/brandbag/`, `/brandwallet-accessories/`, `/brandjewelry/`, `/brandwatch/`), 50+ items/page.
- **Jackroad**: server-side rendered search (30 items/page), brand extraction from title prefix.

Both sources are public web data; only factual product information (name, price, brand, condition rank) is collected.
