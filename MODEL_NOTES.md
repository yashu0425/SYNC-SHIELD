# SYNC-SHIELD v8 — model methods and boundaries

## Source-derived demand

Airtel case: 100,000 fans, 40% Airtel users, 18% simultaneous activity, 70% 5G-capable phones, 5 Mbps NR and 3 Mbps LTE.

- Active Airtel users = 100,000 × 0.40 × 0.18 = 7,200.
- NR demand = 7,200 × 0.70 × 5 = 25,200 Mbps.
- LTE demand = 7,200 × 0.30 × 3 = 6,480 Mbps.

## PRB-based model

Capacity per equivalent cell (Mbps) = PRBs × 12 × SCS_MHz × effective spectral efficiency (bits/s/Hz) × 0.80.

- NR (100 MHz, 30 kHz spacing): 273 PRBs (3GPP TS 38.104); `273 × 12 × .03 × 6 × .8 = 471.744 Mbps`.
- LTE: 350 **hypothetically pooled** PRBs across the case's three LTE bands. `350 × 12 × .015 × 3 × .8 = 151.2 Mbps`. All 350 PRBs per real LTE cell are NOT established by the workbook.
- Required = 54 NR and 43 LTE equivalent sectors.
- Existing 8 NR and 14 LTE equivalent sectors are based on unlabeled `5G 8 / 4G 14` entries in workbook S3:T4. This is a working interpretation, not an independently confirmed installed-cell inventory.
- Planned NR = 8 existing + 34 new small cells + (2 COW × 3 NR sectors) + (2 macro upgrades × 3 new NR sectors) = **54**.
- Planned LTE = 14 existing + 23 new LTE-capable small cells + (2 COW × 3 LTE sectors) = **43**.
- Base model PRB utilisation = 79.139% NR and 79.734% LTE, as *aggregate equivalent-cell estimates*, not measured per-site PRBs.
- At NR efficiency η = 5 bps/Hz, the required NR count increases to 65; base 54 fails. The ₹13L reserve cannot fund 11 additional standard small cells. Do not claim robust acceptance under this condition.

## Backhaul / transport model

- The four existing n78 macros M1/M2/M3/M5 have **10 Gbps fibre each**. These are separate links, not a guaranteed pooled 40Gbps shared service. Candidate distribution of new small cells: NR `[9,9,8,8]` and LTE `[6,6,6,5]` across those four parents. At 80% PRB radio load, incremental user traffic would be about `[5.15,5.15,4.68,4.53]` Gbps respectively. Including illustrative existing macro radio load gives about `[6.40,6.40,5.93,5.78]` Gbps/site. Requires field-verification of spare bandwidth, routing, aggregation hardware, optics and permissions.
- M4/M6 transport: each existing **2Gbps microwave**. Three new NR and two existing LTE equivalent sectors at modelled 80% PRB loading would contribute **1.717632 Gbps/site** user traffic (about 86% of nominal microwave line rate). Airtel specifies 80% PRB radio loading, not 80% transport loading. Transport may be sufficient by nominal rate but needs overhead/headroom checks. No uncosted transport upgrade is claimed.
- Each assumed 3NR+3LTE COW would need around **1.869Gbps** transport under the model; ≥2.5Gbps of suitable vendor supplied capacity is a provisional target. Confirm at procurement, including any fibre, microwave or cellular relay cost.
- 0.5km fibre route at ₹50 lakh/km is a **provisional allowance** not a surveyed route. Only an actual topology and quote can validate ₹25 lakh.

## Budget

- 34 small cells × ₹8 lakh = ₹272 lakh (dual-RAT capability at this price unverified).
- 2 COW × ₹25 lakh = ₹50 lakh (3NR+3LTE sectors/backhaul unverified).
- 2 conditional macro upgrades × ₹20 lakh = ₹40 lakh **assumed vendor price**, not in case.
- 0.5 km fibre × ₹50 lakh/km = ₹25 lakh **assumed route length**.
- Total ₹387 lakh; ₹13 lakh uncommitted **includes all testing and contingency**.

## 5G access, QoS and user experience

- NSA NR secondary-node addition is not the same as a conventional LTE→NR inter-RAT handover. Inspect LTE RRC setup SR, EN-DC / SgNB addition SR, B1 measurement and TTT, NR RACH, PS drop, actual IRAT handover SR if applicable, eNodeB A3/A5/CIO, supported band combinations and X2 configuration.
- Prioritise LTE load relief (compatible LTE bands, M6 if RF/transport permits) before aggressive eNodeB measurement tuning that could add signalling load.
- Managed merchant/POS QoS where supported; suitable wired/Wi-Fi fallback and UPI Lite where eligible. No universal dedicated network slice or always-available offline payment is assumed.
- Emergency: operator-supported IMS emergency bearer priority and ARP pre-emption where implemented; do not block emergency services through access controls or claim fixed PRB reservation without a cost.
- Negative effects: dense-cell interference, handover ping-pong, UL/backhaul congestion, indoor/outdoor boundary holes, post-match exit surges. Mitigations: PCI/TDD sync, planned tilt and power, handover pilots with rollback, transport checks and phase-based testing.

Targets: individual LTE/NR cell DL and UL PRB below 80%; NR addition success ≥95% (proposed), user 5/3Mbps targets under defined load, mobile-network-related POS transaction failures ≤2% (proposed; bank/network-wide failures not fully operator-controlled).
