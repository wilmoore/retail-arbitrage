# 001. Inline Media and Execution Signal Architecture

Date: 2026-02-08

## Status

Accepted

## Context

The retail arbitrage inventory system uses GitHub as the canonical source for item details and media. A delegate (Danie) with view-only GitHub access creates marketplace listings and needs to report listing URLs back to the owner.

Problems with the original approach:
1. Images displayed as bullet links required "View Raw" or download
2. No visibility into listing status (unlisted/listed/sold)
3. No designated location for listing URLs
4. No way for delegate to update status without GitHub write access
5. No machine-addressable anchors for automated updates

## Decision

We implemented a three-layer architecture:

### 1. Inline Media Rendering
- Convert image links from `- [desc](path)` to table format with `![alt](path)` cells
- Images render directly in GitHub Markdown
- Tables provide structured preview + description columns

### 2. HTML Comment Anchors
- Item anchors: `<!-- ITEM:item-slug -->`
- Signal anchors: `<!-- EXECUTION_SIGNALS:item-slug -->` with closing `<!-- /EXECUTION_SIGNALS -->`
- Anchors are machine-parseable and preserved by GitHub rendering

### 3. External Signals Metadata
- `.signals/` directory contains JSON files per batch
- Schema tracks: status, listingUrl, platform, listedAt, soldAt
- Manifests display placeholder values; agents can inject real values
- Delegate submits URLs via batch messages (not GitHub)

## Consequences

### Positive
- Images render inline without friction
- Clear delegate workflow with batch submission instructions
- Owner can see status at a glance
- Agents can target specific items programmatically
- No GitHub write access required for delegate
- No directory structure changes

### Negative
- Requires external write surface for signal updates (not implemented yet)
- Video files cannot play inline (GitHub limitation)
- Tables increase manifest verbosity

## Alternatives Considered

### Notion/External Doc Tool
Rejected: Adds external dependency, moves source of truth away from GitHub

### GitHub Issues for Tracking
Rejected: Fragments item data across issues and manifests

### Grant Delegate Write Access
Rejected: Security concern, overcomplicated for simple URL updates

### Raw Image URLs in Bullet Lists
Rejected: GitHub renders as links, not inline images

## Related

- Planning: `.plan/.done/refactor-inline-media-external-signals/`
