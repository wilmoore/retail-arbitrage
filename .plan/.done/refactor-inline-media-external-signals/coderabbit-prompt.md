# CodeRabbit Review Prompt

## Summary

This PR refactors inventory manifest pages to improve delegate usability and owner visibility by:
1. Rendering images inline (in tables) instead of as bullet links
2. Adding execution signal placeholders for listing status and URLs
3. Adding delegate instructions for batch URL submissions
4. Creating agent-targetable anchors for automated updates

## Review Focus Areas

### 1. Markdown Rendering
- Verify image syntax `![alt](path)` will render correctly in GitHub
- Check table formatting is consistent across all items
- Confirm relative paths work for images in subdirectories

### 2. HTML Comment Anchors
- Validate anchor format: `<!-- EXECUTION_SIGNALS:item-slug -->`
- Ensure closing tags are paired: `<!-- /EXECUTION_SIGNALS -->`
- Check item anchors: `<!-- ITEM:item-slug -->`
- Confirm anchors are machine-parseable

### 3. Signals Metadata Structure
- Review JSON schema in `.signals/README.md`
- Verify item slugs match between manifests and JSON files
- Check status enum values are consistent

### 4. Delegate Instructions
- Confirm instructions are clear and actionable
- Verify example format is copy-paste friendly
- Check all manifests link to main README instructions

## Files Changed

| File | Change Type | Description |
|------|-------------|-------------|
| `README.md` | Modified | Added delegate instructions section |
| `2026-02-01/manifest.md` | Modified | Inline media, execution signals |
| `2026-02-06/manifest.md` | Modified | Inline media, execution signals |
| `.signals/README.md` | New | Signals schema documentation |
| `.signals/2026-02-01.json` | New | Execution signals for batch 1 |
| `.signals/2026-02-06.json` | New | Execution signals for batch 2 |
| `.plan/backlog.json` | Modified | Added in-progress item |

## Constraints Respected

- NO directory structure changes
- NO write access grants required
- NO manual Markdown edits by delegate
- GitHub remains canonical for media and identity
