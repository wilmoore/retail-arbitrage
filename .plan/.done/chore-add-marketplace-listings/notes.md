# Chore: Add Marketplace Recommendations

**Branch:** `chore/add-marketplace-listings`
**Created:** 2026-02-08

## Scope

Add a "Recommended Marketplaces" section to each item listing with item-specific platform suggestions.

## User Requirements

1. **Location:** New section after "Listing Status" table
2. **Strategy:** Item-specific recommendations based on category
3. **Platforms:** Facebook Marketplace, OfferUp, Craigslist, eBay

## Marketplace Recommendation Strategy

Based on item categories, here are the recommended platforms:

| Category | Primary | Secondary | Rationale |
|----------|---------|-----------|-----------|
| Electronics (laptop, mic) | eBay | FB, OfferUp | eBay has best reach for electronics, buyers expect shipping |
| Bikes | FB, Craigslist | OfferUp | Local pickup preferred, FB has strong bike community |
| Audio/Camera gear | eBay | FB, OfferUp | Tech buyers on eBay, local sales on FB |
| Camping/Outdoor | FB, OfferUp | Craigslist | Local outdoor communities |
| Home/Kitchen | FB | OfferUp | Quick local sales |
| Bags/Accessories | OfferUp, FB | eBay | Fast local turnover |
| Books | eBay | FB | eBay for specific titles, FB for lots |
| Clothing | FB, OfferUp | Craigslist | Local clothing sales |

## Item-Specific Assignments

### Batch 2026-02-01

1. **HP ZBook Fury** - eBay (primary), FB Marketplace, OfferUp
2. **Trek FX Bike** - FB Marketplace (primary), Craigslist, OfferUp
3. **DJI Mic 2** - eBay (primary), FB Marketplace, OfferUp
4. **Camera Backpack** - FB Marketplace (primary), OfferUp, eBay
5. **USB Condenser Mic** - FB Marketplace (primary), OfferUp, eBay
6. **Knife Set** - FB Marketplace (primary), OfferUp
7. **Flexible Phone Tripod** - FB Marketplace (primary), OfferUp
8. **Selfie Stick/Tripod** - FB Marketplace (primary), OfferUp
9. **Car Charger** - FB Marketplace (primary), OfferUp
10. **Camping Hammock** - FB Marketplace (primary), OfferUp, Craigslist
11. **Camping Pillows** - FB Marketplace (primary), OfferUp
12. **Puma Tote** - FB Marketplace (primary), OfferUp
13. **Poler Duffel** - FB Marketplace (primary), OfferUp
14. **Book Collection** - eBay (primary), FB Marketplace
15. **Men's Clothing** - FB Marketplace (primary), OfferUp, Craigslist

### Batch 2026-02-06

1. **Ozark Trail Camp Stove** - FB Marketplace (primary), OfferUp, Craigslist
2. **Traeger Pellets** - FB Marketplace (primary), OfferUp, Craigslist

## Implementation Steps

1. Add "Recommended Marketplaces" section after each "Listing Status" table
2. Format as simple bullet list with primary/secondary designation
3. Update README with marketplace strategy context
4. Update signals schema README to document multi-platform tracking

## Section Format

```markdown
### Recommended Marketplaces
- **Primary:** Facebook Marketplace
- **Also list on:** OfferUp, Craigslist
```

## Notes

- HP laptop emphasized as priority for eBay listing (higher-value electronics)
- Local pickup items (bike, camping) favor FB/Craigslist
- Electronics with shipping potential favor eBay
