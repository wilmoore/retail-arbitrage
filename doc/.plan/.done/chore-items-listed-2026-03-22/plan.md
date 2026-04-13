# Plan: Items Listed on 2026-03-22

## Goal

Record the items listed on 2026-03-22 into `inventory/` so listing lifecycle tracking is fast and consistent.

## Constraints

- Data entry must take < 60 seconds per item.
- Use `inventory/items/YYYY-MM-DD-slug/item.yaml` + `inventory/items/YYYY-MM-DD-slug/listings.yaml`.
  - Example: `inventory/items/2026-03-22-wooden-barrel-planter/`
- Leave batches (`2026-*/`) and `.signals/` untouched.

## Output

- One new inventory record directory per item.
- Each record has `item.yaml` (item-level metadata) and a single `listings.yaml` (one listing entry per platform used).

## Related ADRs

- `doc/decisions/002-file-based-inventory-tracking.md`
- `doc/decisions/003-inventory-template-defaults.md`
