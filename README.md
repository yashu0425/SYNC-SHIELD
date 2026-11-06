# SYNC-SHIELD — Airtel SYNC Stadium Surge Digital Twin (v6)

**A judge-friendly, interactive capacity and investment model aligned with the simplified seven-slide Airtel SYNC presentation.**

The public home page explains the recommendation in six steps. The linked **Engineering Lab** retains the original detailed network model so the assumptions can be questioned.

## Open the site

Open **[`index.html`](index.html)** in any current desktop or mobile browser, or publish these files to GitHub Pages. No libraries, server, build tools, tokens, login, data collection or internet access are needed to run the HTML.

- **`index.html`** — recommended judge-facing view: the problem, solution, RF *illustration*, PRB math, budget, stress tests and 60-day plan.
- **`engineering-lab.html`** — optional advanced interactive controls for radio efficiency, LTE bandwidth, sector baseline, COW capabilities, user demand, equipment quantities, outage stress and EN-DC diagnosis.
- **`MODEL_NOTES.md`** — methods, original-data boundaries, KPI definitions and assumptions.
- **`README.md`** — these instructions.
- `preview-judge-desktop.png`, `preview-judge-mobile.png`, `preview-rf-after.png` — optional screenshot examples; not required by the website.

## Default answer — matches the judge-ready slides

| Item | Model value | Status |
|---|---:|---|
| Audience | 100,000 | Airtel case |
| Airtel subscribers | 40,000, with 7,200 concurrently active | Case percentages applied |
| NR demand | 25.20 Gbps | Derived from 5,040 × 5 Mbps |
| LTE demand | 6.48 Gbps | Derived from 2,160 × 3 Mbps |
| NR equivalent-sector requirement | 54 | **Assumed** 273 PRBs / cell and effective ηNR=6 b/s/Hz |
| LTE equivalent-sector requirement | 43 | **Assumed** 350 pooled PRBs / cell and ηLTE=3 b/s/Hz |
| Existing baseline | 12 NR / 20 LTE equivalent sectors | **Unverified**, macro-sector assumption |
| New infrastructure | **36 small cells, of which at least 17 dual-RAT**, plus **2 COWs** | Proposed; COW has assumed 3 NR and 3 LTE equivalents |
| New fibre route | **0.5 km** | Budget allowance, not a surveyed route |
| Testing / contingency | ₹20 lakh | Budget allowance |
| Budget | **₹383 lakh / ₹400 lakh** | Calculated using case unit prices and assumptions |
| Aggregate estimated PRB utilisation | **79.14% NR, 79.73% LTE** | Conditional arithmetic; actual per-cell and per-carrier measurements absent |
| Delivery window | 60 days | Airtel case; achievable only if supply, access and permitting work |

This design has **very narrow capacity headroom** (0.274 Gbps NR and 0.022 Gbps LTE at the 80% model limit). It is not a guaranteed network design.

### What to demonstrate to the judges

1. Start at the top: **What failed?** Peak LTE congestion, poor 5G connection success, low NR speed and UPI failures from the previous match.
2. Explain the three countermeasures: **Connect → Stay connected → Protect users**. Use RRC SR, EN-DC addition SR, PS Drop / SCG failure, mobility KPIs and PRB counters to verify outcomes.
3. Toggle **Existing / Proposed** on the schematic. Stress that it is **illustrative**, not a calibrated propagation model or real site map.
4. Show the **54 NR / 43 LTE equivalent cell** derivation and **₹3.83 crore** budget.
5. Click **NR η drops to 5**, **Only 40 MHz LTE**, or **COW has 1 sector**. The arithmetic fails; this demonstrates why field acceptance gates matter.
6. Open the **Engineering Lab** only if someone asks for full counterfactuals or detailed assumptions.

## Upload the files to your existing GitHub repository

1. Extract the ZIP to a folder on your computer. **Do not upload the ZIP itself.**
2. Open the `SYNC-SHIELD` repository and choose **Add file → Upload files**.
3. Upload **`index.html`, `engineering-lab.html`, `README.md`, and `MODEL_NOTES.md`** to the **repository root**; optionally upload the preview PNG files. Replace the older versions of `index.html`, `README.md`, and `MODEL_NOTES.md` and click **Commit changes**.
4. Under **Settings → Pages**, keep **Deploy from a branch → main → /(root)**. This is a static site; no custom domain is required.
5. Use the existing **Visit site** link in Pages. Refresh the site (hard reload if cached). Verify the opening display shows **36 small cells / 2 COWs / ₹3.83 Cr**, the Before/After map changes and the **Engineering Lab** opens.
6. Verify the existing link / QR in Slide 7 still directs to the same `...github.io/SYNC-SHIELD/` repository website. **The repository name and live URL do not change** when you replace the HTML file.

If GitHub creates a nested folder such as `SYNC_SHIELD_GitHub_Upload_v6/index.html` rather than `index.html` at the root, the website will not update correctly. Upload the **contents** of the extracted folder.

## Important limitations

- The Excel workbook provides 32 phase/site observations and an eight-site inventory, **not** true per-cell PRB measurements, stadium coordinates, antenna configurations or full fibre routes.
- Four n78 macro sites are identifiable. Some LTE-only rows also have a 5G-success field; its meaning is uncertain and the twin does **not** treat that as local NR coverage.
- The workbook's unexplained `5G = 8`, `4G = 14` cells are **not confirmed installed-sector counts**. The Engineering Lab lets you explore that interpretation.
- NR 273 PRBs is specific to 100 MHz, 30 kHz SCS. LTE's 350 composite PRBs per equivalent cell and all effective spectral efficiencies are **hypotheses**, not measured availability.
- The COW configuration, number of LTE+NR sectors, dual-RAT small-cell price, transport / power and installation costs require quotations and site survey.
- The RF diagram is only a scenario illustration, and **no actual mobility performance, UPI outcome, RRC SR, PS Drop or per-cell PRB outcome is predicted**.

See **[MODEL_NOTES.md](MODEL_NOTES.md)** for equations, exact assumptions, diagnostics and acceptance criteria.
