# Receipt — Redfin's price-drop member: the basis of the swap (D630, 2026-11-01)

The operator's ruling (b), 2026-11-01: "we should try to always reconstruct imperfect data into as good of data as possible for
our use with acknowledgement and mitigations for its imperfections." This receipt is that acknowledgement. It read data alone:
no return, forecast, score or outcome.

## What swaps

`HOUSING_REDFIN_PRICE_DROPS` (a monthly share of listings with a price drop, stopped at 2026-05-31; its file answers 403 since
2026-10-28) leaves its slot in `CREDIT_PILLAR_COLLATERAL` at a dated cut, and `HOUSING_REDFIN_DC_PRICE_DROPS_4W` (`PERCENT ACTIVE
WITH PRICE DROPS (%)` of Redfin's weekly file, held as 0–1) takes it, on the same sign and 75-day cap. The slot went stale on
2026-08-14. The cut is `REDFIN_PRICE_DROPS_CUT` in `server/services/credit/creditSignals.js`.

## Sources

| Depot row | File | sha256 |
|---|---|---|
| `redfin` 53 | `price_drops/weekly/country.csv`, updated 2026-10-27, 393 rows 2019-04-21 to 2026-10-25 | `d61fc3b9…` |
| `redfin` 52 | `housing_market/monthly/country.csv`, updated 2026-10-07, 177 rows 2012-01-31 to 2026-09-30 | `4def6847…` |
| `redfin` 51 | Redfin's downloads page, the file map and its seasonal notes | `cf375346…` |

The old side is `housing_series`, 173 monthly rows 2012-01-31 to 2026-05-31.

## The two measures, on their overlap

Each old month-end against the 4-week window ending on or up to 6 days before it:

| Read | Value |
|---|---|
| Months paired | 86, 2019-04-30 to 2026-05-31 |
| Mean gap, in points | 1.14 |
| Largest gap | 5.17 points, 2019-09-30 (19.97 against 14.80) |
| Mean signed gap, new less old | −0.25 points |
| At 2026-05-31 | 18.78 new against 20.04 old |
| Correlation of levels, Pearson and rank | 0.961 and 0.958 |

## Imperfections, and what each one gets

| Imperfection | Mitigation |
|---|---|
| A rolling 4-week figure stepped weekly, against a monthly one | The slot reads the last row of each closed month, so it stays a monthly member. A month closes when the next month's first row lands. |
| Active listings against the tracker's listings | Not removable. The overlap above states the gap. |
| The file carries no property-type column; the tracker's rows were All Residential | Not removable, and not tested here. |
| The file does not say whether it is seasonally adjusted | Read from the data: its calendar-month means over 2022–2025 run 11.4 to 19.9, the old series' 12.0 to 19.4. It reads NSA like the old one. |
| A history from 2019-04, against the old 2012-01 | The z base is spliced: the old months through 2019-03, then the closed months of the new file. Only the z sees the old values. |
| A join of two measures | No back-fill: the old id stays stopped and the new id's rows hold the new measure alone. A pillar row names the id it read. |

## Why the base is spliced

The slot's z against the old z, month by month, on three bases:

| z base | Months | Mean gap | Largest | Mean signed | Correlation | At 2026-05-31 (old 1.62) |
|---|---:|---:|---:|---:|---:|---:|
| The new file alone, every row | 50 | 0.335 | 0.876 | −0.174 | 0.870 | 0.744 |
| Old months, then every weekly row | 86 | 0.270 | 1.354 | −0.177 | 0.950 | 0.980 |
| **Old months, then each closed month (taken)** | 86 | 0.270 | 1.255 | −0.007 | 0.944 | 1.548 |

The taken base carries no signed drift across the join. The weekly form weights recent years four times over and drags the z down.

## What it does to the pillar

- **Inside the old member's life:** with the slot read the taken way on the stored rows, 381 Fridays from 2019-05-03 to 2026-08-14,
  the pillar moves 0.039 on average and 0.179 at most, against the pillar's standard deviation of 0.367.
- **A step at the cut:** the slot has been empty since 2026-08-14, and the new member's z at the last closed month (2026-09-27) reads
  2.00. On the 11 Fridays since, it would have lifted the pillar by 0.18 on average. So expect a step of that size in the first row.
  It comes from the slot refilling, not from the join. Coverage rises by a tenth, to 0.7 on the newest rows, which sit on the 0.6 floor.

## What stays

Read on a scratch copy of the real inputs, the code before and after: 34,697 `credit_signals` rows equal in every field, 0 written,
and the 3,644 pillar rows equal the stored ones. With the new file's rows added and the clock past the cut, 0 stored rows moved.

`registry-composite`'s members, feature, coefficients, gate and stored rows are unchanged. The block pages read the pillar through
`config/block_regimes.yaml` with the same lag, and the field's `regimes.yaml` does not read it.

## The monthly file, for the record

The block's 8.2-day gap on days on market reproduces (8.16, sale-to-list 0.46 points, 173 months), and most of it is not a level
gap: the page says the country monthly leg is seasonally adjusted, and only Median Sale Price stays NSA. Its calendar-month means
run 37.8 to 42.0 where the old series runs 31.5 to 51.5. So `HOUSING_REDFIN_DC_DOM` and `HOUSING_REDFIN_DC_SALE_TO_LIST` are SA where
the old ids are NSA, and they are not spliced into anything. An NSA monthly read exists only through Redfin's page API, not the file
bucket, and the ruling named the two files, so it is not built.
