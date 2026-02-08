# Refactor: Inline Media + External Execution Signals

## Summary

Transform inventory manifest pages to improve delegate usability and owner visibility by:
1. Rendering media inline (images embedded, videos linked)
2. Adding execution signal placeholders (listing status, URLs)
3. Adding delegate instructions for batch submissions
4. Creating agent-targetable anchors for automated updates

## Related ADRs

No existing ADRs found in `doc/decisions/`. This refactor establishes the pattern for:
- Media rendering in GitHub Markdown
- Execution signal architecture
- Delegate handoff workflow

## Analysis

### Current State

**Manifest files use link syntax:**
```markdown
### Images
- [Lid closed - Z logo](images/IMG_15F287E5-648E-4C11-9A23-8639C1C54F66.JPEG) **(PRIMARY)**
- [Open - keyboard view](images/IMG_95D7FFCA-F94E-4EDB-A325-9E666A75D235.JPEG)
```

**Problems:**
1. Clicking opens file view or requires "View Raw" / download
2. No listing status visibility
3. No listing URL location
4. No delegate instructions
5. No machine-addressable anchors

### Target State

**Inline images with raw URLs:**
```markdown
### Images

| Preview | Description |
|---------|-------------|
| ![Primary](images/IMG_15F287E5-648E-4C11-9A23-8639C1C54F66.JPEG) | Lid closed - Z logo **(PRIMARY)** |
| ![](images/IMG_95D7FFCA-F94E-4EDB-A325-9E666A75D235.JPEG) | Open - keyboard view |
```

**Execution signal section:**
```markdown
<!-- EXECUTION_SIGNALS:item-1-hp-zbook -->
### Listing Status

| Field | Value |
|-------|-------|
| **Status** | `UNLISTED` |
| **Listing URL** | _Pending_ |
| **Platform** | — |
| **Listed Date** | — |
<!-- /EXECUTION_SIGNALS -->
```

**Delegate instructions (index page):**
```markdown
## Delegate Instructions

When you complete listings:
1. Create all listings first
2. Collect ALL listing URLs
3. Send URLs in a SINGLE batch message (do not send one-off links)
4. Format: `Item Name: URL`

This enables efficient repo updates.
```

## Implementation Plan

### Phase 1: Update Index Page (README.md)

1. Add delegate instructions section at top
2. Add execution signal columns to batch table
3. Add item-level status indicators

### Phase 2: Update Manifest Templates

For each item in manifest files:
1. Convert image links to inline embeds using raw URL pattern
2. Add execution signals section with HTML comment anchors
3. Add delegate instruction callout per item

### Phase 3: Create Execution Signals Metadata Structure

1. Create `.signals/` directory for execution metadata
2. JSON files per batch: `.signals/2026-02-01.json`
3. Schema for signals:
   ```json
   {
     "items": {
       "item-1-hp-zbook": {
         "status": "unlisted|listed|sold",
         "listingUrl": null,
         "platform": null,
         "listedAt": null,
         "soldAt": null
       }
     }
   }
   ```

## Files to Modify

1. `README.md` - Add delegate instructions, status columns
2. `2026-02-01/manifest.md` - Inline media, execution signals
3. `2026-02-06/manifest.md` - Inline media, execution signals

## Files to Create

1. `.signals/2026-02-01.json` - Execution signals for batch 1
2. `.signals/2026-02-06.json` - Execution signals for batch 2
3. `.signals/README.md` - Documentation for signals structure

## Constraints Respected

- NO directory structure changes (batches stay as-is)
- NO write access grants (signals are read by agent, written via intake)
- NO manual Markdown edits required by delegate
- GitHub remains canonical for media and item identity

## Testing

- Visual verification: images render inline in GitHub
- Anchor verification: HTML comments are preserved and targetable
- Signal injection: placeholder values display correctly

## Implementation Complete

### Files Modified
- `README.md` - Added delegate instructions, status columns
- `2026-02-01/manifest.md` - Inline media tables, execution signals, item anchors
- `2026-02-06/manifest.md` - Inline media tables, execution signals, item anchors

### Files Created
- `.signals/README.md` - Documentation for signals structure
- `.signals/2026-02-01.json` - Execution signals for batch 1
- `.signals/2026-02-06.json` - Execution signals for batch 2

### Key Changes

1. **Inline Media Rendering**
   - Images now use `![alt](path)` syntax in table cells
   - Tables provide preview + description columns
   - Videos linked with download instructions (GitHub limitation)

2. **Execution Signal Anchors**
   - HTML comments: `<!-- EXECUTION_SIGNALS:item-slug -->`
   - Paired closing tags: `<!-- /EXECUTION_SIGNALS -->`
   - Status table between anchors (machine-addressable)

3. **Item Anchors**
   - HTML comments: `<!-- ITEM:item-slug -->`
   - Enables direct linking and programmatic updates

4. **Delegate Instructions**
   - Clear batch submission workflow at top of each manifest
   - Link to main README instructions
   - Example format for URL submissions

## Out of Scope

- External write surface implementation (Supabase, KV, etc.)
- Dashboard or analytics
- Bidirectional sync
- Inventory migration
