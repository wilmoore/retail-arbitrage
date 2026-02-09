# CodeRabbit Review Prompt

## Summary

Added "Recommended Marketplaces" section to all 17 item listings across both batch manifests, providing item-specific platform guidance (Facebook Marketplace, OfferUp, Craigslist, eBay).

## Changes

### README.md
- Updated tagline to "Multi-platform marketplace listings"
- Added "Marketplace Strategy" section with category-to-platform mapping table

### 2026-02-01/manifest.md
- Added "Recommended Marketplaces" section after each item's "Listing Status" table (15 items)
- Item-specific recommendations based on category:
  - Electronics (laptop, mics): eBay primary
  - Bike: FB Marketplace + Craigslist
  - Books: eBay primary
  - Camping/outdoor: FB + OfferUp + Craigslist
  - Bags/accessories/clothing: FB + OfferUp
- Updated "Notes for Lister" to emphasize HP laptop should be listed on eBay

### 2026-02-06/manifest.md
- Added "Recommended Marketplaces" section after each item's "Listing Status" table (2 items)
- Both outdoor items: FB Marketplace + OfferUp + Craigslist

### .signals/README.md
- Extended schema to support `additionalListings` array for multi-platform tracking

### .plan/backlog.json
- Added and completed backlog item for this chore

## Review Focus
1. Consistent section placement (after Listing Status, before Category)
2. Appropriate platform recommendations per item category
3. Schema extensibility for multi-platform tracking
