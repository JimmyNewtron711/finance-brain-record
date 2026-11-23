# D880 — the live sentinels onto D867's v2 lists

*2026-11-17, headless `/resume P1`. The operator's answer, chat, 11-17 ~15:50 ET, verbatim: "D867: yes, and its less about
cyber attacks and more about outages. I dont think attacks will be communicated as much as outages". $0. No price and no
return were read.*

## Frozen before the replay (`73ece8ba`, mirror-pushed before the run)

- **`cyber-incident` `news.deny`** takes D867's `V2_CYBER_DENY` after its 22 forms: `no cyberattack evidence`,
  `no cyber attack evidence`, `no cyber evidence`, `no direct evidence`, `no security breach`.
  `CYBER-INCIDENT-news-burst` stops reading the 11-14 FAA line ("Says No Cyberattack Evidence").
- **`it-outage` `news.doubt`** = `{ entry: cyber-incident, terms: V2_DISRUPTION }`. If `cyber-incident` reads a headline as
  a denial and the headline carries an outage term or one of `issue(s)`, `problem(s)`, `disruption(s)`, then
  `IT-OUTAGE-news-burst` counts it, with no vendor needed. This is D867's `o1v2`: an outage that doubts a cyber cause.
- **v1 does not move.** `systemicScores.js` reads each entry's lists less what D880 added, so `c1` and `o1` keep the D858
  and D859 lists. `tests/systemic-scores.js` T7.2 still pins them.
- **The floor rule:** a switch keeps its floor when v2 holds ≤ 2 episodes a month over the corpus and ≤ 24 in its busiest
  full year. Otherwise the floor is the smallest of 2/3/4/5/6/8/10 that holds.

**The change form is D858's** (taken under the 10-31 filter in `govern/receipts/d858-cyber-denials.md`): each switch keeps
its id, the commit freezes the lists, and the drill on a copy runs before the restart that loads them.

## The replay (`govern/receipts/d880-v2-sentinels-replay.json`)

The replay read 2,303,625 corpus headlines, 2010-03-02 → 2026-11-17, and evaluated each burst's own rule at every hour.
On every headline the live catalogue matcher equals `c1v2` / `o1v2` (0 differ).

| Switch | Headlines | Episodes at its floor | Per month | Busiest full year | Floor |
|---|---|---|---|---|---|
| `CYBER-INCIDENT-news-burst` | 4 out, 0 in | 76 → 75 (1 lost) | 0.37 | 11 | **3, kept** |
| `IT-OUTAGE-news-burst` | 0 out, 12 in | 40 → 42 (2 gained) | 0.21 | 15 | **2, kept** |

- **Cyber lost 2015-07-08:** the NYSE and United outage day. The headlines are "No Security Breach Or Issues" and
  "No Technical Issues On Website, No Security Breach".
- **IT outage gained the same day** (NYSE's "internal technical issue … not the result of a cyber breach") **and
  2021-07-22, Akamai's outage** ("Problems Were Not A Cyberattack").
- **The 12 that join `it-outage`:** CrowdStrike 2024-07-19 (two), FAA 2023-01-11, PGT 2022, Akamai 2021, Colonial
  Pipeline 2021 (two), Twitter 2020, the 2015-07-08 outage day (three) and CNN's 2026-11-13 ground-stop line.
- No threshold is re-tuned.

## The drill (`govern/chokepoints/drills/v2-sentinels-2026-11-17.json`)

The drill ran on a `.backup` copy of `data/dashboard.db`: **PASS, 6 of 6.**
- `computeChokepointNews` ran over 13 entries and 193 hours.
- Every other entry's settled hours read as before: 1,837 rows, 0 differ.
- `cyber-incident`: count plus reverse is as before in each of 167 hours, and 1 headline moved to reverse.
- `it-outage`: no hour's count is lower, and 1 headline was added.
- Both bursts read and evaluate on the copy:
  - `CYBER-INCIDENT-news-burst` is BURST, 3 vs bar 3. The live switch was already BURST (`hormuz_alerts` #358, 11-17 17:00
    ET), on Equinor's "Detects Cyberattack on IT Systems" and two breach settlements, so the restart pushes no new alert.
  - `IT-OUTAGE-news-burst` is QUIET, 9 vs bar 12.
