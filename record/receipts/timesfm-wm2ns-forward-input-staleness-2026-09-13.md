# timesfm-wm2ns-forward — input staleness finding (2026-09-13)

**Finding:** WM2NS read STALE 41 d in stream-health on 2026-09-13 (allowed 28 d). Cause = vendor release cadence, not a
fetcher defect.

- `fred_history` max(date) for WM2NS: 2026-08-03 — equal to FRED's own `observation_end` 2026-08-03 (`last_updated`
  2026-08-25 12:01 CT), read via the FRED series endpoint 2026-09-13 and re-read unchanged 2026-09-14.
- The Federal Reserve H.6 Money Stock release publishes on the fourth Tuesday of every month at 13:00 ET
  (federalreserve.gov/releases/h6). Weekly observations arrive ≈ 22 d after their week and then nothing for up to 35 d, so
  the worst pre-release age is ≈ 57 d. Next print expected 2026-09-22.
- Stream-health's budget (weekly grace 12 + publication lag 16 = 28 d) red-flagged a healthy feed. Fix: `ALLOWED_DAYS`
  row `WM2NS` = 60 d in `scripts/stream-health.mjs` (architecture hardening Task 2, commit `88a941cc`). A read-only run on
  2026-09-14 (scratch report path) read `WM2NS | weekly | 2026-08-03 | OK | 43d old (allowed 60d) | registry-composite,
  timesfm-wm2ns-forward`.

**Effect on the program:** none on the registered protocol (pins untouched; forward reads 2027-03-07 / 2027-09-07). The
forward ledger simply has no new WM2NS week to score until the H.6 print lands.

**Watch:** if `max(date)` is still 2026-08-03 after the 2026-09-23 06:10 heartbeat, it is a fetcher defect → inbox block.
