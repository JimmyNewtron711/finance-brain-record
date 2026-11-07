# Receipt — Sharadar `funds`: the basis of its total-return history (D617, 2026-11-02)

The inbox ruling 3 (b) of 2026-11-01 (Reviews 721 and 722, "All seven") queues Sharadar `funds` as the multi-asset ETF tape's
history before 2016, "a K1 lift plus a basis receipt". This is the receipt. It reads data alone, under Amendment 2026-09-20 (K1)
(5): no signal, return, score or outcome, and no vendor row (its (2)). Counts, shares, dates and one drift per symbol.
Reproduce with `node scripts/funds-basis.mjs` (its `--self-check` is in the root chain).

## What is read

`funds.closeadj`, Sharadar's close adjusted for splits and distributions, as one-session ratios on the vintage held, for the 22
symbols of `equity_daily_tr` (the 20 of the tape in hand and AGG, BIL). Two comparators, both dividend-adjusted:

- **Alpaca's TR tape** (`equity_daily_tr`, `adjustment=all`), each date's newest vintage with a tomb's NULL dropped, as
  `ladder.js` reads the bond gate; 2016-01-04 →.
- **`fmp-etf.db`**, kind `divadj`, the 20 of the tape (no AGG or BIL), 2009-05-01 → 2015-12-31.

Each pair of common sessions gives each side's one-session ratio; the gap is their absolute difference in bp. The drift is the
log of `funds`' compounded level over the other's across the common span, in bp a year, `funds` less the comparator. A
price-only series would drift by minus the whole distribution yield: on AGG, 392 bp over the year to 2026-10-30 (the D530
block's read of this same table).

- funds: 15836646 rows, 10041 tickers, 1997-12-31 → 2026-10-30, lastupdated ≤ 2026-10-31
- equity_daily_tr: 22 symbols, newest asof 2026-11-02T05:45:18Z
- fmp-etf divadj: 20 symbols, 2009-05-01 → 2015-12-31

## funds against the TR tape, 2016 →

| Symbol | Common span | Pairs | Dates only in funds / only in the TR tape | ≤ 1 bp | ≤ 5 bp | ≤ 25 bp | > 25 bp | Largest, dated | Drift, bp a year |
|---|---|---:|---:|---:|---:|---:|---:|---|---:|
| AGG | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 95.9 % | 99.6 % | 99.9 % | 4 | 2020-03-13, 2020-03-12, 2020-03-16 | 0.72 |
| BIL | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 94.6 % | 100.0 % | 100.0 % | 0 | — | -0.04 |
| DBA | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 35.4 % | 95.7 % | 99.8 % | 5 | 2018-12-26, 2020-03-16, 2020-03-17 | -9.80 |
| DBC | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 38.0 % | 94.2 % | 99.9 % | 3 | 2018-12-26, 2020-03-30, 2020-03-31 | -12.94 |
| EEM | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 55.1 % | 94.6 % | 99.9 % | 2 | 2020-03-17, 2020-03-16 | 0.52 |
| EFA | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 73.8 % | 97.9 % | 99.9 % | 2 | 2020-03-17, 2020-03-16 | 1.12 |
| EMB | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 93.1 % | 99.8 % | 99.9 % | 3 | 2016-08-01, 2020-07-01, 2020-07-27 | 3.74 |
| FXE | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 99.1 % | 100.0 % | 100.0 % | 0 | — | 0.04 |
| FXY | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 99.6 % | 99.9 % | 99.9 % | 2 | 2023-02-02, 2023-02-03 | 0.00 |
| GLD | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 89.3 % | 99.0 % | 99.9 % | 4 | 2020-03-17, 2020-03-16, 2020-03-12 | 0.00 |
| HYG | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 80.2 % | 99.2 % | 99.7 % | 7 | 2020-03-10, 2020-03-09, 2020-03-19 | 3.95 |
| IEF | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 97.3 % | 99.9 % | 100.0 % | 0 | — | 1.41 |
| IWM | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 68.1 % | 93.0 % | 99.6 % | 10 | 2020-03-17, 2020-03-16, 2020-03-19 | 0.52 |
| LQD | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 94.3 % | 99.2 % | 99.7 % | 7 | 2020-03-16, 2020-03-17, 2020-03-19 | 5.21 |
| QQQ | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 97.5 % | 99.9 % | 100.0 % | 0 | — | -1.70 |
| SLV | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 96.1 % | 97.2 % | 99.9 % | 3 | 2020-03-17, 2020-03-16, 2020-05-22 | 0.00 |
| SPY | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 68.3 % | 93.6 % | 99.5 % | 13 | 2020-03-13, 2020-03-12, 2020-03-18 | 9.50 |
| TIP | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 97.5 % | 99.8 % | 100.0 % | 1 | 2016-08-01 | 3.82 |
| TLT | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 96.6 % | 99.7 % | 100.0 % | 0 | — | 1.65 |
| USO | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 94.8 % | 96.3 % | 99.4 % | 16 | 2020-05-01, 2020-05-04, 2020-03-18 | 0.00 |
| UUP | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 48.9 % | 99.7 % | 100.0 % | 0 | — | -0.04 |
| VNQ | 2016-01-04 → 2026-10-30 | 2722 | 0 / 0 | 78.7 % | 96.1 % | 99.8 % | 6 | 2020-03-17, 2020-03-16, 2020-03-10 | -0.52 |

## funds against fmp-etf divadj, before 2016

| Symbol | Common span | Pairs | Dates only in funds / only in fmp-etf | ≤ 1 bp | ≤ 5 bp | ≤ 25 bp | > 25 bp | Largest, dated | Drift, bp a year |
|---|---|---:|---:|---:|---:|---:|---:|---|---:|
| AGG | no common span | | | | | | | | |
| BIL | no common span | | | | | | | | |
| DBA | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 40.9 % | 99.6 % | 99.8 % | 4 | 2011-10-27, 2011-10-28, 2010-11-26 | 0.33 |
| DBC | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 39.1 % | 98.3 % | 99.8 % | 4 | 2010-11-29, 2010-11-26, 2011-10-27 | 0.72 |
| EEM | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 50.7 % | 99.5 % | 99.9 % | 2 | 2010-11-29, 2010-11-26 | -1.28 |
| EFA | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 59.4 % | 99.5 % | 99.7 % | 5 | 2014-07-07, 2014-07-03, 2014-08-19 | -0.68 |
| EMB | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 82.1 % | 99.6 % | 99.6 % | 6 | 2014-08-11, 2014-08-12, 2014-03-31 | -0.08 |
| FXE | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 99.8 % | 99.9 % | 100.0 % | 0 | — | -0.03 |
| FXY | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 100.0 % | 100.0 % | 100.0 % | 0 | — | 0.00 |
| GLD | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 99.6 % | 99.9 % | 100.0 % | 0 | — | 0.00 |
| HYG | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 63.0 % | 99.7 % | 99.9 % | 2 | 2014-08-27, 2014-08-26 | -0.05 |
| IEF | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 92.6 % | 99.9 % | 100.0 % | 0 | — | 0.23 |
| IWM | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 89.4 % | 99.4 % | 99.6 % | 7 | 2009-12-23, 2009-12-22, 2014-07-01 | 0.43 |
| LQD | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 89.5 % | 99.5 % | 99.5 % | 8 | 2014-07-15, 2014-07-14, 2010-01-29 | 0.14 |
| QQQ | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 79.8 % | 99.3 % | 99.8 % | 4 | 2009-07-16, 2009-07-17, 2010-11-29 | 3.55 |
| SLV | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 95.3 % | 99.9 % | 99.9 % | 2 | 2011-10-27, 2011-10-28 | 0.00 |
| SPY | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 98.9 % | 100.0 % | 100.0 % | 0 | — | -0.10 |
| TIP | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 94.4 % | 99.5 % | 99.9 % | 2 | 2014-08-26, 2014-08-27 | -0.10 |
| TLT | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 90.3 % | 99.3 % | 99.4 % | 10 | 2011-10-28, 2011-10-27, 2010-03-31 | 0.44 |
| USO | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 98.5 % | 100.0 % | 100.0 % | 0 | — | 0.00 |
| UUP | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 30.1 % | 99.8 % | 100.0 % | 0 | — | -0.07 |
| VNQ | 2009-05-01 → 2015-12-31 | 1679 | 0 / 0 | 57.3 % | 99.6 % | 99.8 % | 4 | 2014-08-26, 2014-06-23, 2014-08-27 | -1.59 |

## funds' sessions before 2016, against SPY's

| Symbol | First row | Rows to 2015-12-31 | SPY sessions it lacks | Rows on no SPY session | Moves past 15 % | Their dates (first four) |
|---|---|---:|---:|---:|---:|---|
| AGG | 2003-09-29 | 3087 | 0 | 0 | 0 | — |
| BIL | 2007-05-30 | 2165 | 0 | 0 | 0 | — |
| DBA | 2007-01-05 | 2264 | 0 | 0 | 0 | — |
| DBC | 2006-02-06 | 2494 | 0 | 0 | 0 | — |
| EEM | 2003-04-14 | 3203 | 0 | 0 | 3 | 2008-10-13, 2008-10-15, 2008-10-28 |
| EFA | 2001-08-27 | 3609 | 0 | 0 | 1 | 2008-10-13 |
| EMB | 2007-12-19 | 2023 | 0 | 0 | 0 | — |
| FXE | 2005-12-12 | 2531 | 0 | 0 | 0 | — |
| FXY | 2007-02-13 | 2238 | 0 | 0 | 0 | — |
| GLD | 2004-11-18 | 2799 | 0 | 0 | 0 | — |
| HYG | 2007-04-11 | 2199 | 0 | 0 | 0 | — |
| IEF | 2002-07-30 | 3381 | 0 | 0 | 0 | — |
| IWM | 2000-05-26 | 3924 | 0 | 0 | 0 | — |
| LQD | 2002-07-30 | 3381 | 0 | 0 | 0 | — |
| QQQ | 1999-03-10 | 4232 | 0 | 0 | 1 | 2001-01-03 |
| SLV | 2006-04-28 | 2437 | 0 | 0 | 1 | 2008-10-10 |
| SPY | 1997-12-31 | 4530 | 0 | 0 | 0 | — |
| TIP | 2003-12-05 | 3039 | 0 | 0 | 0 | — |
| TLT | 2002-07-30 | 3381 | 0 | 0 | 0 | — |
| USO | 2006-04-10 | 2450 | 0 | 0 | 0 | — |
| UUP | 2007-03-01 | 2227 | 0 | 0 | 0 | — |
| VNQ | 2004-09-29 | 2835 | 0 | 0 | 4 | 2008-10-28, 2008-11-24, 2008-12-01, 2009-03-23 |

## What it says

- **`closeadj` is a total-return basis.** Against the TR tape the drift is inside ±13 bp a year on all 22, and inside ±2 bp on 15;
  against `fmp-etf` it is inside ±3.6 bp a year on all 20. AGG's is 0.72 a year, where its price alone parted by 392 bp in the last year.
- **No session is lost.** On the TR tape's span all 22 hold the same 2,723 sessions, none on one side only; against `fmp-etf` the
  same 1,680. Before 2016 no symbol lacks a SPY session from its first row or holds a row off one.
- **One-session moves agree to the cent, not the basis point.** At least 93.0 % of pairs sit within 5 bp of the TR tape's on every
  symbol, and 98.3 % of `fmp-etf`'s. The share within 1 bp is low where the price is low (DBA, DBC, UUP near $20–30, where a
  cent is 3–5 bp): rounding, not basis.

## Imperfections, and what each one gets

| Imperfection | Mitigation |
|---|---|
| A few sessions part by more than 25 bp (at most 16 of 2,722, USO): most in 2020-03 against the TR tape; 2010-11, 2011-10 and 2014-07/08 against `fmp-etf`; mostly two adjacent dates | Read as a close taken at a different print, undone the next session, which the small drifts bear out; the cause is not read here. A pair that undoes itself leaves a monthly read untouched. Not removable. |
| DBA and DBC drift −9.8 and −12.9 bp a year against the TR tape, with their largest gap on 2018-12-26 | The likely cause is their annual December distribution, adjusted differently by the two vendors; not verified here. Before 2016 the same two read 0.3 and 0.7 against `fmp-etf`, so the lean sits after 2016, outside the line's use. Stated, not corrected. |
| SPY drifts 9.5 bp a year against the TR tape and −0.1 against `fmp-etf` | The two total-return tapes part by about 1 % over ten years on SPY; the cause is not read here. Not this receipt's to settle: the line's use is before 2016, where SPY agrees with `fmp-etf`. |
| AGG and BIL have no comparator before 2016 | Their sessions are complete and they move past 15 % on no session. Their 2016 → basis (0.72 and −0.04 bp a year) is the only cross-check. |
| No comparator at all before 2009-05 | The session read and the moves past 15 % stand in for it: 10 such moves, all on dates of real market stress (2001-01-03 for QQQ; 2008-10 → 2009-03 for EEM, EFA, SLV and VNQ). |
| `closeadj` is re-scaled back through history at each distribution | Ratios are unchanged by a re-scale, so a reader reads ratios on one vintage and never a level across vintages. |
| The join at 2016-01-04 of two vendors | No splice: a reader takes `funds` ratios through 2015-12-31 and the TR tape's from 2016-01-04, and no `funds` row enters `equity_daily_tr` or `equity_daily` (the one-adjustment-basis rule). |

## What stays

Nothing written to any store: the three databases open read-only. No program, pin, book, `claims.json` row or window moves, and
no `govern/windows-read.jsonl` line is owed, since nothing here is a discovery read. Until a K1 line lifts Amendment 2026-09-20
(K1) (5) for `funds`, no signal × outcome statistic reads it.
