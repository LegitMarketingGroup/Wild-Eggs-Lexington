# Wild Eggs Lexington — Google Business Profile Dashboard

A self-contained, stat-heavy dashboard covering 18 months of Google Business Profile
performance for the three Wild Eggs restaurants in Lexington, Kentucky, operated by
Traxx Co.

**Open `index.html` in any browser.** No server, no build step, no dependencies at
runtime. Everything — data, styling, charts, logos — is embedded in the single file.

---

## What it shows

Filter by **location** (all three, or one at a time) and by **period** (last 6 months,
last 12, or the full 18). Every number on the page responds to both.

| Section | Contents |
|---|---|
| Totals | Profile views, customer actions, action rate, recorded searches, website clicks, direction requests, phone calls, menu views, food orders, new reviews and average stars |
| Views and actions | Monthly series, per restaurant when unfiltered |
| What people did | The five recorded action types, sized against each other |
| How people searched | Discovery / Branded / Competitor split, by month, plus the largest discovery terms and the rival names that surfaced a Wild Eggs profile |
| Reviews | New reviews per month with the weighted average star rating |

Every chart has a hover tooltip, keyboard-focusable bars with `aria-label`s, and a
**Table view** toggle so the underlying numbers are readable without the chart.

## The headline numbers (February 2025 – July 2026)

| | Hamburg | Palomar Centre | Tates Creek | Estate |
|---|---:|---:|---:|---:|
| Profile views | 400,390 | 315,678 | 185,380 | **901,448** |
| Customer actions | 30,641 | 21,590 | 12,528 | **64,759** |
| Recorded searches | 262,688 | 205,844 | 138,853 | **607,385** |
| — discovery | 140,837 | 99,668 | 81,239 | 321,744 |
| — branded | 81,924 | 80,705 | 57,614 | 220,243 |
| — competitor | 39,927 | 25,471 | **0** | 65,398 |

Tates Creek opened 21 August 2025, so its series starts mid-period. Its competitor
column is zero in every single month — not low, zero. That is a profile eligibility
gap rather than a demand gap, and it is the single largest unclaimed opportunity in
the account.

## Repository layout

```
├── index.html              the dashboard — this is the deliverable
├── data/
│   ├── monthly.csv         location, month, 9 performance metrics
│   ├── search-terms.csv    location, month, term, searches, category, competitor named
│   └── reviews.csv         location, month, new reviews, average stars
└── build/
    ├── prep_data.py        normalises the raw exports into data/*.csv
    ├── build_dashboard.py  generates index.html from data/*.csv
    └── source/             the raw Google Business Profile exports
```

## Rebuilding

```bash
python3 build/prep_data.py        # raw exports  -> data/*.csv
python3 build/build_dashboard.py  # data/*.csv   -> index.html
```

`prep_data.py` holds the term classifier — the brand-spelling list (including the
misspellings people actually type) and the competitor list used to split searches
three ways. Adding a competitor means adding one line there and re-running both
scripts.

## Data notes

- Google retains profile data from **7 February 2025**. There is nothing before it.
- **Search-term data starts March 2025**, one month later than performance data, so
  search totals cover 17 months where performance covers 18.
- Terms under roughly 15 impressions a month are reported by Google as `0` rather
  than suppressed, so the long tail is understated. Totals here are what Google
  reports, not an estimate of true volume.
- `views_total` is not `views_maps + views_search` in every month; Google reports
  the components separately and they do not always reconcile. The dashboard uses
  `views_total` as published.
- Food orders are recorded by Google only for orders placed through a connected
  provider. The near-zero counts reflect that, not the restaurants' order volume.

## Design decisions

Built to the Legit Marketing Group brand standard: navy `#003057`, Fira Sans, square
corners, white chart surfaces, official logo artwork.

**Series palette** is `#003057` navy (Discovery / primary), `#5E7C99` steel
(Branded / secondary), `#A8550D` warm (Competitor). This was validated for
colour-vision deficiency rather than chosen by eye. The two navy-family colours
originally proposed — `#27598F` and `#5E7C99` — failed the normal-vision separation
floor at ΔE 12.6, so the warm accent the brand reserves for "a single warm highlight"
was brought in for the third series. It also carries meaning: Competitor is the
series that should stand apart, and it is the one that reads zero at Tates Creek.

The palette passes CVD separation (worst adjacent pair ΔE 16.7 deutan, 21.5 tritan),
the normal-vision floor (ΔE 19.0) and contrast against the surface. It fails the
generic lightness-band and chroma-floor checks, which is unavoidable: Legit navy is
a dark, low-chroma brand colour by definition. Brand mandate wins over a generic
aesthetic band; the two checks that govern readability both pass.

**No dark mode.** Deliberate rather than overlooked. The brand permits only navy or
white backgrounds, and a navy-surfaced dark variant could not be stepped to pass CVD
separation without abandoning the brand hues. A validated light mode with a table
view beats an unvalidated dark one.

---

Legit Marketing Group · data through July 2026
