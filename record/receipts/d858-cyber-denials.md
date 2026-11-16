# D858 — `systemic_disruption_v1` S0: the `cyber-incident` sentinel's denial fix

*2026-11-15, headless `/resume P1`. Spec `docs/superpowers/specs/2026-11-15-systemic-disruption-score-design.md` § 3 S0
(`65461df8`); the defect is union 758's report, `docs/research/2026-11-14-systems-chokepoints-deep-research.md`,
"Defects in the current catalogue". $0. No price and no return were read.*

## The defect, observed

The report could not say whether the burst had flipped on a denial ("the headline tables sit behind the database
fence"). It did. In `hormuz_alerts`, read-only: #307 `CYBER-INCIDENT-news-burst` QUIET → BURST at **2026-11-14 02:00
ET** (value 3, bar 3), push **sent**; #313 BURST → QUIET at 11-15 01:00 ET. The two corpus headlines in that bucket are
the FAA ground stop's denials (CNN 11-13 21:52Z "…This Is Not A Cyberattack…", Yahoo 11-14 18:11Z "…no sign of
cyberattack"). Under the fix the replay loses that episode (below).

## The fix (`99d18f35`, frozen before the replay)

- `config/chokepoints/cyber-incident.json` `news.deny`, 22 phrases matched whole and case-blind (`termsRegex`):
  - the spec's eight: `denies`, `denied`, `rules out`, `ruled out`, `no evidence of`, `not a cyber`,
    `not caused by a cyber`, `unrelated to a cyber`;
  - fourteen forms seen before the freeze in a read-only scan of the corpus's 895 term-matched headlines
    (`.review-scratch/d858/scan.mjs`) and in the report's quotes: `no evidence`, `no indication`, `no sign of`,
    `not a cyberattack`, `not caused by cyberattack`, `not caused by a cyberattack`, `not a security incident`,
    `not due to a cyber`, `not the result of a cyber`, `not related to ransomware`, `unrelated to the ransomware`,
    `doesn't appear to be a cyber`, `rejects false`, `false alarm`. The spec's `not a cyber` stops at a word boundary, so
    alone it never matches "Not A Cyberattack".
- A headline that matches an entry's terms and its `news.deny` goes to `chokepoint_news_hourly.dashboard_reverse` /
  `corpus_reverse`, never to `tagged` / `corpus_tagged`, so no burst reads it. The reverse tally is the falsification
  input the report's admission criterion 8 asks for. No other entry carries `news.deny`, and each counts as before.

**The change form (taken under the 10-31 filter; reversible by an inbox block).** The spec names "a `-v2` freeze like
D806's, with a drill receipt before the switch is re-enabled". D806's form is a trigger file's. An alert switch of a
sentinel has no trigger file, no `FROZEN` row and no enable flag, and C4 keeps every sentinel switch's file, id and state.
So the switch keeps its id. The list is frozen by the commit that holds it (`99d18f35`, mirror-pushed before the replay
ran), a change to it is a new commit with its own replay, and the drill below ran on a copy before the restart that
loads the code. The restart stands in for the re-enable.

## The replay (`govern/receipts/d858-cyber-denials-replay.json`)

`node orient/investigations/d858-cyber-denials.mjs replay`: every corpus headline, 2010-03-02 → 2026-11-15 (2,299,087
rows), and the switch's own rule (24 h buckets, 168 h, 3×, floor 3) at each of 146,256 hours, before and after.
- **895 headlines match the terms. 28 move to reverse.**
- **82 burst episodes before, 75 after: 8 lost, 1 gained.** The gained one (2021-05-14, 1 h) is a lower baseline once the
  Colonial Pipeline website denial left it.
- The 8 lost: the 2016 White House "false alarm"; Pakistan's central bank denying a breach (2018); **Garmin 2020-07-27, a
  real attack** (its "no indication customer data was accessed"); Colonial Pipeline's website note "unrelated to the
  ransomware" (2021-05-11); the 2023-01-11 FAA NOTAM outage (two episodes, White House "no evidence"); CrowdStrike
  2024-07-19 ("not a security incident or cyberattack"); and **the 11-14 FAA ground stop**, the episode that pushed.
- **Six of the 28 are misfiles,** real incidents or commentary that carry a denial phrase: Garmin 2020, Equifax 2018 and
  PGT 2022 ("no evidence"/"no indication" of data access), F5 2025 ("no evidence of critical exploits"), the Russian envoy
  denying a role in a real attack (2021) and the FBI's "no evidence Russia is trying to stop ransomware attacks" (2021).
  Only Garmin's cost an episode. A narrower v2 (a phrase bound to the cyber term) is possible; it would be a new commit and
  replay, and is not proposed here.

## The drill (`govern/chokepoints/drills/cyber-incident-news-burst-2026-11-15.json`)

`node orient/investigations/d858-cyber-denials.mjs drill` on a `.backup` copy of `data/dashboard.db` (the drill's first
run failed its own entry-count check, which expected 15; 12 entries have terms, and the check now counts them from the
catalogue; re-run): **PASS, 6 of 6.**
- The start adds both columns.
- `computeChokepointNews` ran: 12 entries, 193 hours.
- Every other entry's settled hours read as before: 1,837 rows, 0 differ, reverse 0.
- Each cyber-incident hour's count plus its reverse equals the old count: 167 hours, 4 headlines moved.
- The switch reads and evaluates on the copy (QUIET, 0 in 24 h vs bar 3).
- The source has no reverse column (the live server had not restarted).

## Corrections the report names, made beside the records

The forecast log's correction form is a new forecast id (headline spec, "Registration"). For a basis line it would put f2
in the Brier twice and land f8 LATE, and `tests/event-forecasts.js` E.1 refuses a third kind of line. So both are
corrected here, and the log is untouched: `node scripts/event-forecasts.mjs check` reads 12 forecasts, all OK. (Taken
under the 10-31 filter.)
- **`faa-2026-11-ground-stop-f2`'s basis**, "Cybersecurity names rose after hours on the outage headlines", was found in
  no source either lane read. The after-hours moves reported are LHX −4.2 % and airlines −1.3 % to −2.4 %. The question,
  p and resolution stand; it resolves on prices (D847).
- **`nvda-2026-11-ceo-exit-f8`'s basis** names "the Senate record request (11-17)" as pressure for speed. That letter
  (Warren and Coons) directs Lutnick, Rubio and Miller to preserve records. It is aimed at the administration, not at
  Nvidia.
- **The headline spec's resignation date:** a dated correction line under its line 23 (`99d18f35`). The board accepted
  the resignation effective 11-11 (the 8-K's date of report), and the announcement came on 11-12. Nothing reads the date.
