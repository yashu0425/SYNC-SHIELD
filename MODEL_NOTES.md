# SYNC-SHIELD v6 — Methodology, Assumptions & Limitations

## Two-view architecture

- `index.html` is the **judge-facing overview** matching the simplified PPT narrative. It uses the same historical workbook data and base-case arithmetic as the Engineering Lab but intentionally reduces the technical display.
- `engineering-lab.html` is the **advanced decision model**; it contains the full adjustable hardware, radio, transport and failure assumptions. Both files work offline.
- All maps are schematic and cannot predict actual RF field strength, interference or per-zone loading.

## Evidence from the case

- Case: 100,000 spectators; 40% Airtel market share; 70% 5G-capable; 18% peak concurrent; 5 Mbps 5G, 3 Mbps 4G; 100 MHz n78, 70 MHz LTE across 3 bands; limit of 80% loading; total budget ₹400 lakh; cost ₹8L/small cell, ₹25L/COW/event, ₹50L/km new fibre.
- Network history: 32 site-phase KPI observations. At the previous match's innings break, average LTE B3 load of the seven busy sites ~98.5% while M6 was ~60.5%. Four actual n78 macro sites M1/M2/M3/M5 had ~36.2% reported 5G connection success. UPI failure 7.11% vs 1.23% normal day.
- M4/M6 2 Gbps microwave; M1/M2/M3/M5 10 Gbps fibre. LTE-only rows carry a populated 5G-success field: treat its meaning as **unclear**, not evidence of NR present at those sites.

## Calculations

Peak subscribers `100000 × .40 = 40000`, active `40000 × .18 = 7200`, NR-capable `7200 × .70 = 5040`, LTE-only `2160`. Peak demands: `5040 × 5 = 25200 Mbps NR` and `2160 × 3 = 6480 Mbps LTE`.

### 5G PRB calculation

Assume 30 kHz n78 subcarrier spacing. A 100 MHz NR channel contains 273 PRBs under 3GPP TS 38.104. One PRB occupies `12 × 30 kHz = 360 kHz = 0.36 MHz`. With assumed effective spectral efficiency η_NR = 6 bits/s/Hz (including TDD fraction and other applicable overhead), 80%-loaded sector data capacity is `273 × 0.36 × 6 × .8 = 471.744 Mbps`. Required `ceil(25200/471.744)=54` equivalent NR sectors. Sensitivity: η_NR 5 → 65; η_NR 4 → 81.

### LTE PRB calculation

LTE uses 15 kHz SCS: one PRB = `12×15 kHz = 180 kHz = 0.18 MHz`. The 70 MHz LTE **case total** is spread across 3 bands; the illustrative optimistic model assumes that the equivalent cell can utilise 350 composite downlink PRBs (e.g., suitable multi-carrier configuration; LTE 20 MHz 100 PRBs, LTE 10 MHz 50 PRBs). Actual carriers, frequency availability by site, duplexing and device capability are missing. With assumed effective η_LTE =3 bits/s/Hz, capacity at 80% is `350×0.18×3×.8 =151.2 Mbps`. Required `ceil(6480/151.2)=43` LTE equivalents. At only 40 MHz/200 PRB, the required LTE cell count increases sharply.

### Conditional baseline / deployment

Assume three sectors per macro site: 4 n78 macro =12 existing NR equivalents; 6 LTE macro =18 plus 2 existing LTE-only small cells =20 LTE. Thus needs additional **42 NR / 23 LTE**. Build 36 one-sector n78 small cells, at least 17 also LTE capable, plus two assumed 3-NR +3-LTE COWs. Total **54 NR / 43 LTE equivalents**.

Aggregate model NR PRB occupancy `25200 / (54×273×0.36×6) = 79.138968%`; LTE `6480/(43×350×0.18×3)=79.734219%`. Capacity at 80% = 25.474 Gbps NR and 6.502 Gbps LTE, only +0.274 Gbps and +0.022 Gbps above demand. These are pooled arithmetic values; **no actual cell's scheduled PRB counter is available** and spatial hotspots could exceed 80% even if pooled totals pass.

Alternative undocumented Excel entries `5G = 8`, `4G = 14` are not labelled as existing radio sectors. If they were existing equivalents, preferred design would fail; the twin includes this alternative baseline as a stress test.

### Budget and field conditions

- Small cells: 36×₹8L = ₹288L
- Two COWs: 2×₹25L = ₹50L
- New fibre: assumed 0.5 km×₹50L/km = ₹25L
- Testing/contingency: assumed ₹20L
- Total ₹383L; remaining ₹17L

Risks: case ₹8L small-cell unit cost does not explicitly promise dual-RAT; case ₹25L COW does not promise 3+3 sectors or backhaul; .5 km fibre not surveyed; 60-day permits/power/transport/OEM readiness not verified. Do not infer geographic RF reach from the illustrative map. No new small-cell or COW site backhaul cap is verifiable from the provided information.

## KPIs and corrective control logic

- **RRC SR** = successful RRC establishment ÷ RRC attempts ×100, for LTE accessibility.
- **PS Drop** = operator-defined abnormal packet-service release / drop ratio; inspect E-RAB/DRB and EN-DC SCG failure counters to interpret retainability. Definition varies by vendor and service.
- **SgNB addition SR** = successful secondary gNB additions ÷ requests ×100; primary NSA 5G addition KPI. The sheet's headline 5G success figure may have another definition — request metadata.
- **IRAT HOSR** = actual inter-RAT handover successes ÷ attempts ×100; apply if a 4G→NR handover procedure exists (not interchangeable with NSA SgNB addition).
- **DL/UL PRB occupancy** = scheduled resource blocks over sampled intervals ÷ available resource blocks over same intervals ×100, measured separately per cell and configured carrier. Require less than 80% under defined high-load tests.

Candidate eNodeB changes to test **after diagnosis**: B1-NR measurement threshold, hysteresis and time-to-trigger; LTE A3/A5 offsets and CIO; compatible LTE anchor combinations, neighbour/X2 definitions and SgNB admission; LTE load steering and NR RACH/SCG error diagnostics. No fixed setting values are justified without site counter trends, drive tests and a rollback plan.

## Functional zones and testing

Bowl and stands: dense users at innings break. Food stalls: RRC, data access, low packet loss, merchant wired/managed Wi-Fi support. Gates/parking/exits: transient crowds, weak edge RF and handover routes. The spatial map illustrates priorities only. Validate UPI network-caused errors separately from bank/payment-app failures. Check IMS emergency calls and supported fallback. Stress the actual system against lower η, 90% NR served fraction, fewer COW sectors, less LTE PRB allocation, single macro outage, and 25% concurrency. Avoid claiming site-outage resilience from an aggregate spreadsheet model.

## Standards

- NR 273-PRB config: 3GPP TS38.104 Table 5.3.2-1 (100MHz, 30kHz).
- LTE PRBs: 20MHz=100, 10MHz=50 under LTE waveform configurations; 12 subcarriers at 15kHz per PRB.
- LTE RRC and NR Event B1: TS36.331. EN-DC SgNB addition: TS37.340.
