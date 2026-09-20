# Catalogue anchors — fetched 2026-09-14 (spec 2026-09-14-novel-hypothesis-lane-design.md §2.3 step 1)

| anchor | URL | status | bytes | raw id | entries to key |
|---|---|---|---|---|---|
| osap-signaldoc.csv | https://raw.githubusercontent.com/OpenSourceAP/CrossSection/master/SignalDoc.csv | 200 | 181712 | 1 | 331 data rows (212 Predictor, 114 Placebo, 5 Drop) |
| hxz2020-replicating-anomalies.pdf | https://global-q.org/uploads/1/2/2/6/122679606/houxuezhang2020rfs.pdf | 200 | 859985 | 2 | Appendix A, pages 54–106 |
| hlz2016-factor-list.xlsx | https://people.duke.edu/~charvey/Factor-List.xlsx | 200 | 422519 | 3 | sheet1 434 rows |
| quantpedia-screener.html | https://quantpedia.com/screener/ | 200 | 641495 | 4 | 82 visible strategies |

Raw bytes: `data/raw/catalogue/payloads.db` (append-only). Extracted copies under `.review-scratch/catalogue/anchors/` are working
files, never tracked.

Measured against plan-time figures (spec §6 P5): OSAP `SignalDoc.csv` parses to 331 rows / 29 columns with no embedded newlines
(plan time recorded 514 from a WebFetch read; the fetched file's last column is `GScholarCites202509`), so its keying batches are
lines 2–91, 92–181, 182–271, 272–332; Quantpedia's server-rendered screener carries 82 distinct `#NNNN` symbols (plan time 75).
HXZ Appendix A runs PDF pages 54–106 (Appendix B starts on page 107); HLZ sheet1 matches plan time (434).
