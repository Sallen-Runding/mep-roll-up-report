# MEP Private Equity Deal Tracker

Living, institutional-grade tracker of **commercial** U.S. private-equity consolidation across the MEP contractor market. Residential deals are out of scope.

**Current version:** 1.2 · **Baseline:** Jan 1, 2025 → Jul 6, 2026

## Repository structure

```
.
├── data/
│   └── deals.json      ← SINGLE SOURCE OF TRUTH. Edit this file to update the tracker.
├── docs/               ← published site (GitHub Pages / Azure Static Web Apps root)
│   ├── index.html      ← self-contained brief; reads deals.json and renders all 4 sections
│   ├── deals.json      ← copy of data/deals.json, kept alongside index.html for the fetch
│   └── MEP_PE_Deal_Tracker.md   ← human-readable markdown master (generated from deals.json)
├── pdf/
│   └── MEP_PE_Deal_Tracker_v1.2_Commercial.pdf   ← distribution PDF for team proofing
└── README.md
```

## The four sections
1. **Master Deal Tracker** — full dataset, one row per transaction
2. **Top 5 Deals** — signal over volume, each with a "why it matters"
3. **Top 10 Snapshot** — clean distribution table, no analysis
4. **Platform & Sponsor Intelligence** — active roll-ups, new platforms, recaps, structural indicators

## How to update (Phase 2 workflow)
1. Edit **`data/deals.json`** only — add or amend entries in the `deals` array; update `top5`, `top10`, `meta.counts`, and append to `changelog`.
2. Copy it alongside the site: `cp data/deals.json docs/deals.json`
3. Commit and push. `index.html` re-renders automatically from the new data.

### Data rules (enforced in every update)
- **Verified public sources only.** Blanks over estimates.
- **Employee counts:** only where explicitly stated in a credible source. Never estimated or inferred.
- **Transaction Date:** the date the deal was announced or closed per the cited source. `date_basis` records announced / completed / closed / advisor-disclosed; `date_precision` records exact / month / year.
- **Cumulative versioning:** rows are never deleted — only archived or annotated.
- **Source priority:** PRNewswire, Business Wire, Newsfile, Notified, PrivSource, PE Hub, CT Acquisitions, Capstone Partners, ACHR News, Consulting-Specifying Engineer, Mechanical Hub.

## Hosting (recommended architecture)
GitHub (source of truth) → Azure Static Web Apps (auto-deploy on push, app root = `/docs`) → iframe embed in the Webflow `/private-equity` page.

Example embed:
```html
<iframe src="https://YOUR-AZURE-STATIC-APP-URL/index.html"
        style="width:100%;height:1600px;border:0;" loading="lazy"
        title="MEP Private Equity Deal Tracker"></iframe>
```

If you use **GitHub Pages** instead: Settings → Pages → Source = `main` branch, `/docs` folder. The site publishes at `https://USERNAME.github.io/REPO/`.

## Notes
- `index.html` is fully self-contained (no build step, no dependencies) and fetches `deals.json` from the same directory, falling back to `../data/deals.json`.
- The PDF is a static snapshot of v1.2; regenerate it when the dataset changes materially.
