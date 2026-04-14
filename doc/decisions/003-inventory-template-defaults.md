# 003. Inventory Template Defaults

Date: 2026-04-13

## Status

Accepted

## Context

The file-based inventory system is designed for very fast entry and quick backfills.

During early usage, we found two sources of accidental inconsistency:

- Unknown acquisition fields were sometimes stored as empty strings and sometimes as null.
- New listing records could be created with missing platform/URL but marked as active, which is misleading when the listing has not been posted or linked yet.

## Decision

- Represent unknown acquisition fields as null (not empty strings).
- Default new listing entries to status "draft".
- Promote a listing to status "active" only when platform and URL (or other identifying posting info) are known.

## Consequences

- Inventory YAML is more consistent and easier to scan/search.
- Draft listings reduce confusion and avoid reporting a listing as live when it is not fully captured.
- Requires one extra step to mark a listing active once posting details are available.

## Alternatives Considered

- Keep empty strings for unknown values: rejected due to inconsistency and awkward filtering.
- Keep status active by default: rejected because it misrepresents incomplete listings.
- Add strict schema validation: deferred to keep data entry under 60 seconds.

## Related

- ADR: `doc/decisions/002-file-based-inventory-tracking.md`
- Planning: `doc/.plan/.done/chore-items-listed-2026-03-22/`
