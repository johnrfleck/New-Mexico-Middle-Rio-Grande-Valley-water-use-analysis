# Domestic Wells — methodology

Under New Mexico state statute, residents are permitted to drill a domestic well for household use
with little regulatory oversight. The result in New Mexico's Middle Rio Grande Valley is a growing
shift of water use away from more expensive, scarce, and tightly regulated water uses such as
surface irrigation diversions and municipal supplies to domestic wells. Residents must apply for a
permit to drill a well, but issuance is automatic, and there is no metering of the resulting
diversion of water.

While the New Mexico Office of State Engineer publishes a geospatial dataset identifying well
permits and locations, many of the locations are only imprecisely known, making analysis of
spatial patterns in well locations and therefore the resulting consumptive use of water
challenging. Without metering, there is no way to ground truth the amount of water being
withdrawn. Without precise location data, it also is difficult to know *where* the use is
happening.

Attempts to overcome those problems, in part by using remote sensing data, can nevertheless
provide insights which, while lacking precision, are better than the current information vacuum
that has left domestic wells outside the Middle Rio Grande Valley's current water management
framework.

This note summarizes how we have pursued this question in the domestic-wells replication notebook
(`notebooks/domestic_wells/domestic_wells_replication.ipynb`) which provides our best conservative estimate of the number of wells located in key management jurisdictional areas. The notebook is the
source of truth; this is a plain-language overview.

## Question

The core question is how many domestic wells, categorized as “active” by the New Mexico Office of State Engineer, are located inside the boundaries of the Middle Rio Grande Conservancy District jurisdictional area and the Albuquerque Bernalillo County Water Utility Authority service area, and what are the legally permitted diversions from those wells.

We have chosen these areas for two reasons. The MRGCD jurisdictional boundary provides a good proxy for the Middle Rio Grande Valley floor, where shallow aquifers make well drilling and groundwater pumping cheap. The ABCWUA service area represents an area where expensive, regulated water is available through the municipal system, but domestic well users opt for cheaper and unregulated water for outdoor irrigation. The result is a concentration of what appear to be areas of rising consumptive water use in those parts of the greater Albuquerque urban area where domestic wells are common, while consumptive water use is declining in much of the urban area served only by municipal water.

The resulting pattern, identified in the work that follows, is residential lots with domestic wells that tend to be larger and greener, meaning with higher water use per acre, than those limited to ABCWUA supplies.

## Published result (OSE POD vintage 2026-06-15)

| Boundary | Domestic wells | Permitted diversion |
|---|--:|--:|
| MRGCD | 22,916 | 63,477 acre-feet/yr |
| ABCWUA | 7,901 | 22,465 acre-feet/yr |

## The counting ladder

Wells are counted in four steps. The gaps between them are the modeling choices, made explicit:

1. **Active domestic PODs** — active OSE points of diversion with a domestic use code
   (`DOM`, `DOL`, `PDM`, `DCN`) whose location falls inside the boundary.
2. **Physical well locations** — drop OSE administrative records (`CLW` change-of-location filings
   and `-X` administrative suffixes) that are not new wells on the ground.
3. **Unique water rights** — a reference count. Multiple wellheads of one right are deduplicated to
   the base right (`RG-NNNNN`), and the right's permitted diversion is counted once (its AF is shared
   across its `-POD2 / -POD3` wellheads). (MRGCD 24,239 / ABCWUA 8,557.)
4. **Unique rights, solidly inside** — **the headline.** Drops boundary-ambiguous
   PLSS-centroid stacks: a confirmed stack of ≥10 co-located wells (no quarter-quarter refinement)
   is counted only when its entire ~1-square-mile section box is inside the boundary; stacks whose
   box straddles the line are dropped, because we cannot confirm those wells are inside. This is the
   conservative, published number (MRGCD 22,916 / ABCWUA 7,901).

## Key caveats

- **Permitted, not consumed.** `total_div` is the permitted annual diversion — an administrative
  ceiling, not measured pumping or consumptive use.
- **POD location quality.** Most OSE coordinates are PLSS-cell centroids, not field GPS. The analysis
  only tests point-in-boundary and makes no parcel-level claims. Parcel-level analysis can be found in the notebooks that follow this one.
- **ABCWUA boundary is provisional.** The OSE Public Water System polygon (used here) and ABCWUA's own
  service-zone map disagree by ~1,200 rights; the OSE polygon is the more conservative choice. See
  `data/domestic_wells/README.md`.
- **Vintage-dependent.** A newer OSE POD download will shift the counts.
