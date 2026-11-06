# SYNC-SHIELD v8 — Airtel SYNC Stadium Surge

A standalone, mobile-responsive, browser-based **planning digital twin** aligned to the audited 7-slide Airtel SYNC v8 presentation.

Open `index.html` on your computer, or upload `index.html`, `engineering-lab.html`, `README.md`, and `MODEL_NOTES.md` into the root of the existing GitHub Pages repository.

## Reference scenario

- 100,000 attendees; Airtel share 40%; 18% simultaneous activity; 70% 5G devices.
- Working spreadsheet baseline: **8 existing NR** + **14 existing LTE equivalent cells** (unlabeled workbook helper entries, to be verified).
- New design: **34 small cells** (23 need LTE and NR capability), **2 COWs** (3 NR + 3 LTE sectors per COW assumed), **2 conditional n78 macro upgrades** (3 new NR sectors each assumed).
- NR 54 equivalents; LTE 43 equivalents; modelled aggregate PRB load 79.14% NR, 79.73% LTE.
- Budget ₹272L + ₹50L + ₹40L (assumed macro price) + ₹25L (assumed 0.5km fibre) = ₹387L; ₹13L balance includes testing and contingency.
- Hardware capabilities, prices, backhaul routes and RF quality must be confirmed before implementation.

## Website controls

- Before / After RF **illustrative** stadium view, including food stalls, parking and gates.
- Engineering Lab allows NR spectral efficiency, LTE PRB pool, existing baseline, concurrency, COW sector count and small-cell quantity to vary.
- The model displays **failures openly**; ηNR=5 under the base design fails 80% PRB criteria.

## Publish

1. On GitHub, replace the old repository-root `index.html` and `engineering-lab.html`, plus `README.md` and `MODEL_NOTES.md` with these files.
2. Commit changes to `main`.
3. In Settings → Pages, continue with Deploy from branch `main` and `/(root)`.
4. Check the published homepage from an incognito browser. It should show **34 small cells + 2 COWs + 2 macro upgrades; ₹3.87 Cr**.

Not an RF propagation predictor; not real-time Airtel RAN telemetry; contains no analytics or remote service dependencies.
