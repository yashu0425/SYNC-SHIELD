# Model methodology and assumption register

## Sources (supplied by the case participant)

- `Airtel_SYNC_Network_Case_Study.pdf`: Stadium Surge, pp. 2–3.
- `Sync_V1.xlsx`: site inventory, previous-match measurements, UPI outcomes, and unlabeled worksheet values.
- `Airtel_SYNC_SHIELD_Final_Reviewed_Aligned.pptx`: reviewed seven-slide submission, to which this demo is aligned.

## Exact demand formulas

```text
active_subscribers = spectators × 0.40 × concurrent_percentage × phase_factor
NR_served_users = active_subscribers × 0.70 × NR_served_percentage
LTE_served_users = active_subscribers − NR_served_users
NR_demand_Gbps = NR_served_users × 5 / 1000
LTE_demand_Gbps = LTE_served_users × 3 / 1000
```

Base: spectators=100,000, concurrency=18%, phase_factor=1 at innings break, 100% of active 5G-capable users served on NR. NR demand = **25.20 Gbps**, LTE demand = **6.48 Gbps**. The NR-served fraction is **not** the measured NR connection-attempt success KPI, which cannot be directly translated into served users.

Illustrative phase multipliers are 0.64 crowd buildup, 1.00 innings break, 1.00 final over and 0.82 post-match. These factors are **assumptions**; Airtel provides no phase-wise active-user counts.

## Equivalent radio-cell capacity

```text
NR_each_Gbps = 100 MHz × effective_NR_bpsHz × 0.80 × (1 − additional_loss/100) / 1000
LTE_each_Gbps = usable_LTE_MHz × effective_LTE_bpsHz × 0.80 × (1 − additional_loss/100) / 1000

NR_count = existing_NR + NR_small_cells + (COW_count × assumed_NR_sectors_per_COW) + (3 × optional_macro_upgrades)
LTE_count = existing_LTE + dual_RAT_small_cells + (COW_count × assumed_LTE_sectors_per_COW)
```

- The default assumes **100 MHz n78 NR** is available for each NR equivalent sector and **70 MHz LTE** for each LTE equivalent sector. Airtel states **70 MHz across three LTE bands**; per-cell LTE availability has not been verified.
- Assumed *effective* (overheads included) efficiencies are 6 b/s/Hz NR and 3 b/s/Hz LTE. Actual RF performance could differ significantly. Do **not** apply another TDD/overhead factor if efficiencies are already effective.
- Airtel asks to plan maximum **80%** radio load. This factor is applied once to each radio equivalent sector's assumed capacity.
- Existing default counts: 4 n78 macros × 3 NR sectors = 12 NR; six LTE macros × 3 LTE sectors + two LTE-only small cells = 20 LTE. These are modelling assumptions, not recorded sector counts.
- Alternate inventory: 8 NR and 14 LTE from worksheet cells that have **no explanatory headings**. This alternative is provided as a test only, not a confirmed interpretation.
- A COW is assumed to provide 3 NR and 3 LTE sectors in the base. A single-sector-per-technology option is included because the case price does not specify COW radio capabilities.
- Macro upgrades are optional, not recommended by the deck. If selected, ₹20L per upgrade is **not a case price**. For upgraded M4/M6 only, the model limits planned total LTE+NR transport to 80% of 2 Gbps microwave per site until upgrade is verified. Site traffic, uplink and backhaul sharing are not simulated packet-by-packet.
- Planned sector counts do not establish actual geographic coverage, UE association, neighbour compatibility, EN-DC accessibility, uplink, or actual user rate quantiles.

## Budget formula

```text
cost_lakh = (8 × small_cells) + (25 × COWs) + (50 × assumed_fibre_km)
           + (20 × optional_macro_upgrades) + testing_allowance_lakh
```

- `₹8L/small cell`, `₹25L/COW per event`, and `₹50L/km new fibre` are case prices.
- Additional dual-RAT capability for 13 of the 35 small cells at **no incremental price** is a **major unverified assumption**.
- `0.5 km` new fibre and `₹20L` testing allowance are candidate budget allowances, not measured installation requirements.
- Existing spare fibre access capacity and COW backhaul are **not provided**; cost and feasibility may be understated. No inferred or guaranteed path lengths.

### Three PPT-aligned candidate configurations

| Model candidate | NR small | LTE+NR small | COWs | NR equivalents | LTE equivalents | Cost |
|---|---:|---:|---:|---:|---:|---:|
| Fibre-first | 41 | 19 | 0 | 53 | 39 | ₹373L |
| **Hybrid A (preferred in reviewed deck)** | **35** | **13** | **2** | **53** | **39** | **₹375L** |
| Hybrid B | 32 | 10 | 3 | 53 | 39 | ₹376L |

All assume 12 existing NR, 20 existing LTE, 3+3 per COW, 0.5 km new fibre and ₹20L testing. Equivalent total radio counts are **not** geographically guaranteed coverage.

### Near-zero capacity margins in the preferred case

```text
NR planned = (12 + 35 + 2×3) × 0.480 = 25.440 Gbps ; demand = 25.200 → +0.240
LTE planned = (20 + 13 + 2×3) × 0.168 = 6.552 Gbps ; demand = 6.480 → +0.072
```

Consequently, even a small decline in effective spectral efficiency, fewer usable LTE bands, a macro outage, a different baseline sector count, or single-sector COWs may invalidate the arithmetic. These scenarios are exposed in the *Failure laboratory*.

## Stadium-zone diagram

The schematic highlights seating bowl, food stalls/payments, internal gates, parking and outer entry/exit clusters. For visual clarity, only *representative new-cell cluster markers* are plotted. The 35 proposed permanent small cells are allocated in a **purely illustrative** 60% / 25% / remaining zone split (21 bowl / 9 concourse-food / 5 internal gates). COW placement is conceptual. Neither the colours nor the layout is a measured RSRP/SINR propagation map. Actual placement needs surveyed geometry, crowd density, antenna design, power, fibre, and RF simulations / measurements.

## 5G connection diagnostic

The *EN-DC failure detective* shows hypothetical step probabilities for LTE access, NR measurement, SgNB admission/X2, NR random access and retention. It calibrates the product of step probabilities to the observed mean **36.2%** headline connection KPI across the four n78 macro sites at the previous innings break. It does **not** attribute failures to any particular stage or forecast the success of repairs; the supplied workbook lacks stage-specific counters. Unmeasured n78 success entries on LTE-only sites are not presented as local 5G availability.

## Geographical and transport limits

The simulator does not compute path loss, RSRP, SINR, TDD UL/DL scheduling, per-zone load distribution, sector adjacency/interference, detailed backhaul uplink/downlink routing, accurate COW antenna beams, real handovers, live user throughput, or UPI transaction failure probability. It therefore reports only **aggregate model arithmetic**, never a true radio-engineering acceptance certificate or proof of 60-day commissioning feasibility.
