[Google Maps Reviews Scraper](https://apify.com/scrape.badger/google-maps-reviews-scraper?fpr=data)

## What does Google Maps Reviews Scraper do?

Scrape reviews for many Google Maps places in a single Apify run. Reviews-only micro-actor — accepts one OR many `place_ids` / `data_ids`, with sort order and topic filter.

## Why use Google Maps Reviews Scraper?

- **Batch input.** Paste a list of place_ids (one per line or comma-separated) — no need to configure a separate task per place.
- **Sort & filter.** `mostRelevant` / `newestFirst` / `highestRating` / `lowestRating` + optional topic keyword filter.
- **Per-place pagination budget.** `max_pages_per_place` (1-50) caps credit spend when batching many places.
- **Single-purpose UI.** No `mode` dropdown, no fields you'd never use — just reviews.
- **Cheapest reviews-only actor on Apify.** $0.30 / 1k reviews — see benchmark.

## What data can Google Maps Reviews Scraper extract?

| Field | Type | Description |
| --- | --- | --- |
| place_id | string | Source place ID (stamped onto every review for correlation) |
| author | string | Reviewer display name |
| author_url | string | Reviewer Google profile |
| rating | number | Star rating (1-5) |
| published_at | string | ISO 8601 timestamp |
| text | string | Review body |
| topics | array | Google-extracted topic tags |
| likes | number | Helpful votes |
| owner_response | object | Merchant reply (text + timestamp), when present |

## How to scrape Google Maps

1. Click **Try for free**.
2. Paste one or many Google Place IDs into the **Place IDs** box (one per line, or comma-separated).
3. Optional: set `sort_by`, `topic_id`, `gl`, `hl`.
4. Set `max_pages_per_place` — each page ≈ 10 reviews.
5. Click **Start** — reviews stream into the dataset, tagged with the source place_id.

## How much will it cost?

**$0.003 per review page (≈ $0.30 per 1,000 reviews).** One credit-equivalent per API call; each page returns ≈ 10 reviews. Batching 100 places at `max_pages_per_place: 3` = 300 calls = $0.90.

### Competitor benchmark

| Actor | Author | Price | Notes |
| --- | --- | --- | --- |
| compass/google-maps-reviews-scraper | Compass | ~$7 / 1k places (reviews bundled) | Reviews come with full place crawl |
| apify/google-maps-reviews-scraper | Apify | ~$0.60 / 1k reviews | Official Apify actor |
| lukas_krivka/google-reviews-scraper | Lukas Krivka | ~$0.40 / 1k reviews | Community favourite |
| **scrape-badger/google-maps-reviews-scraper** | **ScrapeBadger** | **$0.30 / 1k reviews** | **Batch place_ids + topic filter** |

## Input

Configure the run in the **Input** tab above, or pass a JSON object matching the fields below when calling the Actor via the Apify API.

| Field | Required | Description |
| --- | --- | --- |
| place_ids | ✅ (or `data_ids`) | One place ID per line, or comma-separated. |
| data_ids | ✅ (or `place_ids`) | Alternative: one data_id per line. |
| sort_by | — | `mostRelevant` / `newestFirst` / `highestRating` / `lowestRating`. |
| topic_id | — | Topic keyword (`service`, `food`, `atmosphere` …). |
| gl / hl | — | Country + language. |
| max_pages_per_place | — | 1-50, default 5. |

## Output

Every successful run streams records into the run's dataset. Download as JSON, CSV, XML, Excel, or HTML from the **Dataset** tab; consume programmatically via the Apify API or webhooks.

Example record:

```
{
  "place_id": "ChIJ_3Su08fj5UYRkFfNoiuWQUk",
  "author": "Jane Doe",
  "rating": 5,
  "published_at": "2026-04-15T10:23:00Z",
  "text": "Best flat white in midtown. Staff remembered my name on visit two.",
  "topics": [
    "coffee",
    "atmosphere"
  ],
  "likes": 3,
  "owner_response": {
    "text": "Thanks, Jane!",
    "published_at": "2026-04-16T09:00:00Z"
  }
}
```

## Tips / Advanced options

- **Pipe from `google-maps-scraper`.** Run Search Places first, copy the `place_id` column, paste here.
- **Use `sort_by: newestFirst` for monitoring.** Set on a daily cron to catch new reviews.
- **`topic_id` is case-sensitive.** Use the exact topic string Google surfaced in its own topic chips.
- **Failed places are stamped, not hidden.** A not-found place emits one `{status: empty, reason: not_found}` record — easy to filter out downstream.

## FAQ, Disclaimers, Support

### Can I use place URLs instead of IDs?

Not directly — extract the `ChIJ…` or `0x…:0x…` segment from the URL first. `google-maps-scraper` Search Places mode returns both.

### What's the max batch size?

Apify's own runtime limits apply (memory, disk). ≈ 500-1000 places per run is comfortable at 256 MB; more than that, chunk into multiple runs.

### Does this include owner responses?

Yes, when Google returns them, as the `owner_response` field.

### Why stamp the place_id on each review?

So you can group / correlate downstream when the dataset mixes reviews from many places.

### Disclaimer

This Actor scrapes public Google data only. You're responsible for compliance with Google's Terms of Service and any applicable data-protection laws (GDPR, CCPA, etc.) in your jurisdiction. ScrapeBadger does not store the scraped results — they are delivered directly to your Apify dataset.

### Support

Something not working? Open a ticket in the **Issues** tab above — we triage within one business day. Full API reference: [docs.scrapebadger.com](https://docs.scrapebadger.com).

### Related Actors

- [`google-maps-scraper`](https://apify.com/scrape-badger/google-maps-scraper) — Full multi-mode (search + place + reviews + photos + posts)
- [`google-maps-photos-scraper`](https://apify.com/scrape-badger/google-maps-photos-scraper) — Photos-only twin of this actor

### Powered by

[ScrapeBadger](https://scrapebadger.com) — Google-optimised residential proxy pool + browser-farm fallback, 99.7% uptime, unmetered bandwidth. No CAPTCHAs reach you.