# 002. File-Based Inventory Tracking

Date: 2026-03-22

## Status

Accepted

## Context

The repository started as a one-time batch listing workflow (batch manifests + `.signals/`). The work has shifted to ongoing, intentional listing and relisting, with a need to track:

- what is listed
- where it is listed
- how long it has been listed
- list price vs sold price
- lightweight performance signals

We want "database semantics without the database": fast capture, human-editable files, and a git audit trail.

## Decision

Introduce an `inventory/` directory as the system-of-record for all new items going forward.

- Keep the existing batch manifest + `.signals/` system unchanged for historical batches.
- Represent each item as a record directory: `inventory/items/<date-slug>/`.
- Store item metadata in `inventory/items/<date-slug>/item.yaml`.
- Store all listings for that item in a single `inventory/items/<date-slug>/listings.yaml` file.
- Prefer schema-last evolution: start with simple templates and expand fields only when real usage requires it.

## Consequences

### Positive

- New items can be captured quickly (target: < 60 seconds per item).
- One place to track list vs sold price and listing age across platforms.
- Records are self-contained and easy to move/archive.

### Negative

- No automated reporting or validation initially.
- Over time, `listings.yaml` may get large for high-churn items (can be split later if needed).

## Alternatives Considered

### Migrate all existing batches into inventory

Rejected for now: higher effort and risk without proven benefit.

### Keep using only manifests + `.signals/`

Rejected: the batch workflow is optimized for delegation, not ongoing lifecycle tracking and economics.

### Use a spreadsheet or database

Rejected: either loses structured git history (spreadsheet) or adds infrastructure/migrations/tooling overhead (database).

## Related

- Planning: `doc/.plan/.done/feat-add-file-based-item-tracking/`
- Prior ADR: `doc/decisions/001-inline-media-execution-signals.md`
