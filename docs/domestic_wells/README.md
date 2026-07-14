# Domestic Wells — methodology

This note summarizes how the domestic-wells replication notebook
(`notebooks/domestic_wells/domestic_wells_replication.ipynb`) counts wells. The notebook is the
source of truth; this is a plain-language overview.

## Question

The core question is how many domestic wells, categorized as “active” by the New Mexico Office of State Engineer, are located inside the boundaries of the Middle Rio Grande Conservancy District jurisdictional area and the Albuquerque Bernalillo County Water Utility Authority service area, and what are the legally permitted diversions from those wells.



## Published result (OSE POD vintage 2026-06-15)

| Boundary | Domestic wells | Permitted diversion |
|---|--:|--:|
| MRGCD | 24,239 | 67,389 acre-feet/yr |
| ABCWUA | 8,557 | 24,406 acre-feet/yr |

## The counting ladder

Wells are counted in four steps. The gaps between them are the modeling choices, made explicit:

1. **Active domestic PODs** — active OSE points of diversion with a domestic use code
   (`DOM`, `DOL`, `PDM`, `DCN`) whose location falls inside the boundary.
2. **Physical well locations** — drop OSE administrative records (`CLW` change-of-location filings
   and `-X` administrative suffixes) that are not new wells on the ground.
3. **Unique water rights** — **the headline.** Multiple wellheads of one right are deduplicated to
   the base right (`RG-NNNNN`), and the right's permitted diversion is counted once (its AF is shared
   across its `-POD2 / -POD3` wellheads).
4. **Unique rights, solidly inside** — a robustness check that drops boundary-ambiguous
   PLSS-centroid stacks (a confirmed stack of ≥10 co-located wells whose ~1-square-mile section could
   straddle the boundary line). Reported for transparency; it moves the headline only slightly
   (MRGCD 24,239 → 22,916; ABCWUA 8,557 → 7,901).

## Key caveats

- **Permitted, not consumed.** `total_div` is the permitted annual diversion — an administrative
  ceiling, not measured pumping or consumptive use.
- **POD location quality.** Most OSE coordinates are PLSS-cell centroids, not field GPS. The analysis
  only tests point-in-boundary and makes no parcel-level claims.
- **ABCWUA boundary is provisional.** The OSE Public Water System polygon (used here) and ABCWUA's own
  service-zone map disagree by ~1,200 rights; the OSE polygon is the more conservative choice. See
  `data/domestic_wells/README.md`.
- **Vintage-dependent.** A newer OSE POD download will shift the counts.
