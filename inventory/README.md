# Inventory (File-Based Tracking)

This folder is an ongoing, file-based tracking system for items you list and sell.

It is designed to complement (not replace) the existing batch manifests (e.g. `2026-02-01/manifest.md`) and `.signals/` execution metadata.

## Structure

Each item is a self-contained record directory:

```
inventory/items/<item-id>/
  item.yaml
  listings.yaml
```

## Item IDs

Use date-prefixed IDs for natural sorting:

- `YYYY-MM-DD-<slug>`

Example:

- `2026-03-22-sony-wh1000xm4`

## Create a New Item

1. Create a directory: `inventory/items/<item-id>/`
2. Create `item.yaml` from `inventory/templates/item.yaml`
3. When you post listings, update `listings.yaml` using `inventory/templates/listings.yaml`

## Update Workflow

- When you repost/edit a listing: update that listing's `updated_at` and `status`.
- When you check messages: update `metrics.last_checked` and increment `metrics.inquiries` as needed.
- When the item sells: set `status: sold` and fill `sale.*` fields.

## Field Conventions

- Dates: ISO date recommended (`YYYY-MM-DD`).
- Money: numbers only (no `$`).
- Listing status values: `active`, `sold`, `delisted`, `expired`, `draft`.

## Notes

- Keep currency fields as numbers (no `$`) so later scripts can compute totals.
- Prefer ISO dates: `YYYY-MM-DD`.
- Avoid storing sensitive customer data; use minimal identifiers.
