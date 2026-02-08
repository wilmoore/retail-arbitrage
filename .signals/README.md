# Execution Signals

> External write surface for listing status and URLs

This directory contains execution metadata that tracks listing status without requiring direct Markdown edits.

## Schema

Each batch has a corresponding JSON file:

```json
{
  "batchId": "2026-02-01",
  "lastUpdated": "2026-02-08T14:30:00Z",
  "items": {
    "item-slug": {
      "status": "unlisted|listed|sold",
      "listingUrl": "https://...",
      "platform": "facebook|offerup|craigslist|ebay",
      "listedAt": "ISO-8601",
      "soldAt": "ISO-8601"
    }
  }
}
```

## Item Slugs

Item slugs are derived from item numbers and names:
- `item-1-hp-zbook-fury`
- `item-2-trek-fx-hybrid-bike`
- `item-3-dji-mic-2`

## Update Flow

1. Delegate creates listings on marketplace
2. Delegate sends batch of URLs to owner/agent
3. Agent updates corresponding `.signals/*.json` file
4. Manifest pages reference signals for status display

## Status Values

| Status | Meaning |
|--------|---------|
| `unlisted` | Not yet listed on any marketplace |
| `listed` | Active listing exists |
| `sold` | Item has been sold |
| `hold` | Listing paused (e.g., awaiting authorization) |
