# Japan Luxury Brand Market — Cross-Shop Price Comparison

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

## Pricing

Pay per event — $0.00005/run + **$0.002/item**.

## Data source notes

- **Komehyo**: server-side rendered category pages (`/brandbag/`, `/brandwallet-accessories/`, `/brandjewelry/`, `/brandwatch/`), 50+ items/page.
- **Jackroad**: server-side rendered search (30 items/page), brand extraction from title prefix.

Both sources are public web data; only factual product information (name, price, brand, condition rank) is collected.
