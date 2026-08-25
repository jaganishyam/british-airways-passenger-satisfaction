# Data dictionary — `ba_cleaned.xlsx`

**1,324 rows x 26 columns.** Reviews published March 2016 – October 2023.

Columns 1–19 come from the source review data; columns 20–26 are fields derived during cleaning to
support time-series, sentiment and banding analysis in Tableau.

| Column | Type | Nulls | Description | Values |
|---|---|---|---|---|
| `header` | str | 0 (0.0%) | Review headline written by the passenger | 1,300 distinct values |
| `author` | str | 0 (0.0%) | Reviewer display name as posted publicly | 833 distinct values |
| `date` | datetime64[us] | 0 (0.0%) | Date the review was published | 938 distinct values |
| `place` | str | 0 (0.0%) | Reviewer country — joined to countries.csv for continent/region | 56 distinct values |
| `content` | str | 0 (0.0%) | Full free-text review body | 1,324 distinct values |
| `aircraft` | object | 0 (0.0%) | Aircraft type, consolidated into 11 groups in Tableau | 150 distinct values |
| `traveller_type` | str | 0 (0.0%) | Business, Solo Leisure, Couple Leisure or Family Leisure | Business, Couple Leisure, Family Leisure, Solo Leisure, Unknown |
| `seat_type` | str | 0 (0.0%) | Cabin class flown | Business Class, Economy Class, First Class, Premium Economy |
| `route` | str | 0 (0.0%) | Origin to destination, including via points | 836 distinct values |
| `date_flown` | datetime64[us] | 0 (0.0%) | Month the flight took place | 88 distinct values |
| `recommended` | str | 0 (0.0%) | Would the passenger recommend BA (yes/no) | no, yes |
| `trip_verified` | str | 0 (0.0%) | Whether the review platform verified the trip | Not Verified, Verified |
| `rating` | int64 | 0 (0.0%) | Overall rating, 1–10 | min 1, max 10, mean 4.19 |
| `seat_comfort` | float64 | 11 (0.8%) | Seat comfort rating, 1–5 | min 1, max 5, mean 2.90 |
| `cabin_staff_service` | float64 | 11 (0.8%) | Cabin crew rating, 1–5 | min 1, max 5, mean 3.32 |
| `food_beverages` | float64 | 100 (7.6%) | Food and beverage rating, 1–5 | min 1, max 5, mean 2.66 |
| `ground_service` | float64 | 4 (0.3%) | Ground service rating, 1–5 | min 1, max 5, mean 3.04 |
| `value_for_money` | int64 | 0 (0.0%) | Value for money rating, 1–5 | min 1, max 5, mean 2.78 |
| `entertainment` | float64 | 457 (34.5%) | In-flight entertainment rating, 1–5 | min 1, max 5, mean 2.72 |
| `review_year` | int64 | 0 (0.0%) | Year extracted from date | 2016, 2017, 2018, 2019, 2020, 2021 |
| `review_month_no` | int64 | 0 (0.0%) | Month number 1–12 | 1, 2, 3, 4, 5, 6 |
| `review_month` | str | 0 (0.0%) | Month name | April, August, December, February, January, July |
| `review_quarter` | str | 0 (0.0%) | Calendar quarter | Q1, Q2, Q3, Q4 |
| `sentiment` | str | 0 (0.0%) | Derived sentiment: Positive / Neutral / Negative | Negative, Neutral, Positive |
| `rating_category` | str | 0 (0.0%) | Derived banding of the overall rating | Average, Excellent, Good, Poor |
| `recommendation` | str | 0 (0.0%) | Derived label of the recommended flag | Not Recommended, Recommended |

## Null-handling notes

- **`entertainment` (457 nulls, 34.5%)** — treated as *not applicable* rather than zero. Many
  short-haul aircraft have no seat-back entertainment, so a null means the service was absent, not
  that it was rated badly. Tableau's `AVG()` excludes nulls, so the reported 2.72 average covers
  only flights that offered entertainment.
- **`food_beverages` (100 nulls, 7.6%)** — same treatment.
- **`seat_comfort`, `cabin_staff_service`, `ground_service`** — under 1% nulls each; no impact on
  aggregate results.
- **`traveller_type`** contains a single `Unknown` row. It is retained for completeness but is too
  small to affect the traveller-type comparison.

## Join

`ba_cleaned.place` -> `countries.csv.Country` (left join), adding `Continent` and `Region`.
All 56 distinct countries in the review data matched, with zero unmatched rows.
