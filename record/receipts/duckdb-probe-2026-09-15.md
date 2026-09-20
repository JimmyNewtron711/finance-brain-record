# DuckDB probe — one month of minute bars, SQLite vs zstd Parquet (2026-09-15)

**Decision (proposal E4 rule): SQLite scan 33.40 s ≤ 10 min → no derived store; close E4.** No dependency added to any
repo venv. Architecture hardening plan Task 9, measurement only.

- **Gate:** `pgrep -f 'node scripts/backfill-minute-bars'` empty; run 01:48:59 → 01:53:58 ET, outside 06:00–06:40.
- **Setup:** scratch venv `mktemp -d` (`/tmp/tmp.AjuWzWnlyR`), Python 3.12.3, `pip install duckdb` → **duckdb 1.5.5**;
  `probe.py` verbatim from the plan (Step 1). Deleted after this receipt (`rm -rf`).
- **Command:** `timeout 5400 $P/venv/bin/python $P/probe.py /home/brain/finance-brain/data/minute-bars.db 1785542400 1788220800 $P/aug.parquet` → `rc 0`
- **Output:** `rows 12751 == 12751 | sqlite scan 33.40s | copy 221.48s | parquet scan 0.04s | parquet 103.0 MB`
  (the plan's row-set assert passed: symbol × UTC day × count identical on both sides).

| measure | value |
|---|---|
| August 2026 rows (`ts` 1785542400 … 1788220800) | 5,129,509 |
| total `minute_bars` rows | 640,250,863 |
| SQLite scan (GROUP BY symbol, day; `session = 1`) | 33.40 s |
| DuckDB `COPY` SQLite → Parquet (zstd) | 221.48 s |
| Parquet scan (same query) | 0.04 s |
| Parquet file | 102,982,422 B (103.0 MB) |
| month's share of the SQLite file (rows / total × 49,353,711,616 B) | 0.8012 % → 395.4 MB |
| Parquet / SQLite share | 0.260 |
| plain `count(*)` month + whole table (sqlite3 CLI, after the probe, both together) | 44 s |

**Reading:** the table is `WITHOUT ROWID` with PK `(symbol, ts)`, so a ts-only range is a full scan of the 49 GB file,
and it still finished in 33 s. Page-cache state was not controlled: dropping caches needs root. The box has 109 GB RAM
with 84 GB in buff/cache, so a cold-cache scan could be slower, but a > 18× slowdown would be needed to cross the
10-minute bar. Parquet is ≈ 800× faster to scan and ≈ 4× smaller, but a month-scale research read already costs
< 1 min in SQLite, so the derived Parquet mirror (a new dependency, its own K1 line and the `test_ro_factory` pin
question) is not proposed. Re-open E4 only if a registered program's scan is measured above 10 min.
