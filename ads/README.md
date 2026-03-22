# Ads (Service Arbitrage CRM)

This folder is a simple, file-based system for storing service ad templates and tracking where they are posted plus lead/job outcomes.

## Create a New Ad
1. Create a new service folder under `ads/` (kebab-case), e.g. `ads/couch-moving/`.
2. Add three files:
   - `ad.md` (reusable copy)
   - `platforms.yaml` (where it is posted)
   - `responses.csv` (leads/jobs log; source of truth)

## Store the Ad Template (`ad.md`)
- Keep a consistent format:
  - `Title:`
  - `Body:`
- Write copy so it can be pasted into multiple platforms with minimal edits.

## Track Platforms (`platforms.yaml`)
- One top-level map: `platforms`.
- Per platform:
  - `posted`: `true`/`false`
  - `url`: live listing URL (if available)
  - `last_posted`: last time it was posted/reposted (ISO date recommended: `YYYY-MM-DD`)
  - `created_at`: first time you posted on that platform (ISO date recommended)
  - `updated_at`: last time you touched/edited the listing (ISO date recommended)
  - `notes`: anything relevant (repost cadence, account constraints, etc.)

## Log Responses and Jobs (`responses.csv`)
Operational rule: every time a lead comes in, append one line to the service’s `responses.csv`. That file is the truth.

Suggested status values: `new`, `replied`, `quoted`, `scheduled`, `completed`, `lost`, `spam`.

Columns:
- `date` (ISO date `YYYY-MM-DD`)
- `platform` (must match a key in `platforms.yaml`)
- `lead_name`
- `phone_or_contact` (phone, email, username, etc.)
- `pickup_area`
- `dropoff_area`
- `quoted_price` (number, no `$`)
- `status`
- `notes`

## Expand Later
Add more service folders under `ads/` (same three-file pattern):
- junk removal
- couch moving
- furniture pickup
- free-item arbitrage
