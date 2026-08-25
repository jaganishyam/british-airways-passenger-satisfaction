# British Airways Passenger Satisfaction Analysis

**Tableau dashboard and CSAT analysis of 1,324 British Airways passenger reviews (2016–2023)**

Only 43% of passengers would recommend British Airways. This project analyses seven years of
passenger reviews to find out why — and ranks which service areas the airline should fix first.

Built end-to-end in Tableau Desktop: **24 worksheets, 3 role-specific dashboards, and a 9-point
narrative story** for stakeholder presentation.

---

## Headline findings

| Question | Finding |
|---|---|
| **Are customers happy?** | No. Average rating **4.19 / 10**, recommendation rate **43.2%**, and **61% of reviews are negative**. |
| **What should BA fix first?** | **Food (2.66/5) → Entertainment (2.72/5) → Value for Money (2.78/5) → Seat Comfort (2.90/5)** — all four sit below the 3.0 midpoint. |
| **Does food really matter?** | Decisively. Passengers rating food 4–5 recommend BA **86%** of the time; those rating it 1–2 recommend **12%**. A **74-point swing**. |
| **Does cabin crew drive satisfaction?** | It barely moves the overall score, but it dominates recommendation: **72%** vs **4.8%** between high and low cabin-staff ratings. |
| **Which cabin performs worst?** | **Business Class (3.93/10) rates below Economy (4.36)** — a paying-premium problem, and the single most commercially urgent finding here. |
| **Which aircraft?** | Airbus **A350 leads (5.37/10)**; **A321 trails (3.71/10)**. No aircraft in the fleet exceeds a 55% recommendation rate. |
| **Who is happiest?** | **Solo Leisure (4.29/10)** travellers; **Family Leisure (3.80/10)** are the most dissatisfied. |

The recurring theme: **BA's problems are on-board and consumable — food, entertainment, seat
comfort — not operational.** Ground service (3.04) and cabin staff (3.32) are the two
highest-scoring metrics, so the weakness is what the airline serves, not how its people serve it.

---

## Business context

British Airways collects CSAT and review data from passengers across countries, routes, aircraft
types and cabin classes. The PR and Customer Experience teams needed that raw feedback turned into
something management could act on.

**Stakeholders this was built for:**

- VP / Managers — Flight Operations
- VP / Managers — Maintenance
- Customer Experience team
- Senior Management

Each of the three dashboards targets one of these audiences rather than serving one dashboard to
everybody.

---

## Dashboards

| # | Dashboard | Audience | Contents |
|---|---|---|---|
| 1 | **Executive Overview** | Senior Management | 5 KPI cards, monthly trend, recommendation donut, rating distribution, sentiment split |
| 2 | **Service Quality** | CX & Maintenance | Service comparison, improvement-priority lollipop, cabin-staff scatter, food box plot, traveller type |
| 3 | **Geography & Aircraft** | Flight Operations | Filled map, top-10 countries, aircraft bar, recommendation treemap, continent slope chart |

All three use **cross-filtering** — clicking any chart filters the rest. On Dashboard 3 the map acts
as a filter, so selecting a country redraws every other chart on the sheet.

The **9-point story** walks a stakeholder from "are customers happy?" through to "what do we fix
first?" in presentation order.

> **Screenshots:** dashboard exports belong in [`images/`](images/). See the note in that folder for
> the two-minute export steps.

---

## Data

| | |
|---|---|
| **Reviews** | 1,324 rows × 26 columns, March 2016 – October 2023 |
| **Coverage** | 56 countries, 11 aircraft groups, 4 cabin classes, 4 traveller types |
| **Lookup** | 251 countries with continent and region |
| **Source** | Publicly posted Skytrax / AirlineQuality passenger reviews |

Full column-by-column reference: **[`docs/data-dictionary.md`](docs/data-dictionary.md)**.

**Data model:** `ba_reviews.place` left-joined to `countries.Country`. All 56 countries in the review
data matched the lookup with **zero unmatched rows** — the join was validated before any geographic
analysis was built.

### Cleaning and preparation decisions

- **`entertainment` — 457 nulls (35%).** Treated as *not applicable* (short-haul aircraft without
  seat-back screens), **not** as zero. Tableau's `AVG()` excludes nulls, so the 2.72 average reflects
  only flights where entertainment actually existed. Coding these as 0 would have manufactured a
  false crisis in the priority ranking.
- **`food_beverages` — 100 nulls (7.5%).** Same treatment.
- **`aircraft` — 100+ inconsistent free-text entries** consolidated into **11 clean groups** using
  Tableau's Group feature, making aircraft-level comparison possible at all.
- **`Review Date`** — calculated field `MAKEDATE([review_year], [review_month_no], 1)` to give the
  trend chart a continuous date axis instead of a discrete text one.
- **Outliers** — frequency analysis on the ordinal rating fields found no evidence that low-frequency
  levels should be excluded, so none were.

**Known limitation:** self-selected online reviews skew negative — unhappy passengers write reviews
more often than satisfied ones. The 4.19/10 average should be read as a *relative* signal for
comparing aircraft, cabins and countries, not as BA's true fleet-wide CSAT.

---

## Repository structure

```
├── data/
│   ├── raw/
│   │   ├── ba_reviews.csv          # 1,324 source reviews
│   │   └── countries.csv           # 251-country continent/region lookup
│   └── processed/
│       └── ba_cleaned.xlsx         # cleaned dataset used by Tableau
├── tableau/
│   ├── british-airways-passenger-satisfaction.twbx   # ← open this
│   └── extract/
│       └── ba_cleaned.hyper        # standalone Tableau extract
├── docs/
│   ├── data-dictionary.md          # all 26 columns, types, nulls, join logic
│   ├── project-documentation.docx  # full build documentation
│   └── business-requirements.docx  # objectives, problems, stakeholders, KPIs
└── images/                         # dashboard screenshots
```

## Opening the workbook

1. Install [Tableau Desktop](https://www.tableau.com/products/desktop) or the free
   [Tableau Public](https://public.tableau.com/app/discover).
2. Open `tableau/british-airways-passenger-satisfaction.twbx`.

The `.twbx` is a **packaged** workbook — the data extract travels inside it, so it opens with no
setup and no broken connections. Built in Tableau Desktop Professional Edition 2026.1.2; older
versions may not open it.

---

## Tools & skills demonstrated

**Tableau Desktop** — calculated fields, groups, parameters, dual-axis charts, filled maps with
geographic roles, cross-filter actions, dashboard actions, story points, custom tooltips, dynamic
titles · **Excel** — data cleaning, type conversion, null handling, deduplication ·
**Analysis** — data modelling and join validation, null-handling strategy, sentiment segmentation,
correlation analysis, priority ranking · **Communication** — stakeholder-segmented dashboard design,
narrative structuring, written documentation

## Recommendations delivered

1. **Fix catering first.** Food is both the lowest-rated metric and the strongest predictor of
   recommendation. It is the highest-leverage intervention available.
2. **Audit the Business Class product.** Rating below Economy while charging a premium is a direct
   revenue risk.
3. **Set entertainment expectations per aircraft** rather than uprating fleet-wide — the metric is
   only meaningful on aircraft that offer it.
4. **Investigate A321 configuration.** Lowest-rated aircraft, consistent with high-density
   narrow-body seating on longer routes.
5. **Protect cabin crew standards.** Crew quality is what still converts passengers into
   recommenders despite the product weaknesses.

---

## Author

**Shyam Jagani** — Data Analyst
[GitHub](https://github.com/YOUR-USERNAME) · [LinkedIn](https://linkedin.com/in/YOUR-LINKEDIN)

## License

[MIT](LICENSE). Review data is publicly posted passenger feedback, included here for educational and
portfolio purposes.
