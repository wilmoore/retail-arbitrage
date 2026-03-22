# Plan: File-Based Item Tracking

## Goal

Create a simple, file-based system (FileStore style) to track items on an ongoing basis:

- what is being listed
- where it is listed
- when it was listed / last updated
- list price vs sold price
- basic performance signals (inquiries, last checked)

Keep the existing batch manifests and `.signals/` approach intact.

## Constraints

- Prefer simple files and directories; avoid overengineering.
- Human-editable; agent-readable.
- Easy to extend later (more fields, multiple listings per item, sales outcomes).

## Approach

- Add `inventory/` as the ongoing system-of-record for new items.
- Use "directory as record": one directory per item.
- Store item metadata in `item.yaml`.
- Store all marketplace listings for the item in a single `listings.yaml` file.
- Store lightweight metrics inside each listing entry.

## Non-Goals (for this pass)

- No automation (reports, make targets, syncing `.signals/`, etc.).
- No migration of existing batch items unless requested.

## Related ADRs

- `doc/decisions/002-file-based-inventory-tracking.md`
