# D859 — the it-outage sentinel (systemic_disruption_v1 S1)

*2026-11-15, headless. Spec: `docs/superpowers/specs/2026-11-15-systemic-disruption-score-design.md` § 3 S1. $0. No price read and no return read.*

## Frozen before the replay (`160ad610`, mirror-pushed before the run)

- **`news.terms`**: 16 outage forms. A read-only corpus scan left out three forms. "is down" and "are down" match a stock's fall ("Why CrowdStrike Stock Is Down Today"), and "glitch" mostly matches a product bug. "went down" was left out too ("How The CEO Succession At Visa Went Down").
- **`news.vendors`**: 48 vendors. They come from the report's top-fifteen rows that name an IT vendor:
  - Microsoft;
  - the hyperscalers;
  - CrowdStrike;
  - Cloudflare, Akamai and Fastly;
  - the airlines and Sabre;
  - the FAA, NOTAM and air traffic control;
  - Change Healthcare, CDK, UKG and Kronos;
  - the carriers and 911;
  - Visa, Mastercard, Fedwire and FedNow;
  - Okta and npm;
  - Coinbase, Binance and Bybit.

  The platform's own vendors are added: GitHub, Anthropic/Claude, Alpaca and Databento. Rows 5 (grids) and 15 (fabs) name no IT vendor. `taiwan-fabs` and `europe-gas` watch parts of those rows. Some names are too broad and are kept narrow: "southwest airlines", never "southwest" (the Southwest's power cuts); no "swift" (it matches "Taking Swift Action").
- **`news.deny`**: "denies", "denied", "did not experience", "no outage". Two corpus headlines move to reverse: T-Mobile's "Did Not Experience An Outage" (2024-02-22) and Amazon's "Denies Reports Of AWS Outage" (2025-11-07). The cyber sentinel's forms ("no evidence of", "not a cyber") are not reused: "FAA outage … no evidence of cyberattack" denies a cause, not the outage.
- **The floor rule**: the smallest floor of 2/3/4/5/6/8/10 (multiple 3, as every sentinel's burst) that gives ≤ 2 episodes a month over the corpus and ≤ 24 in its busiest full calendar year.

## The replay (`govern/receipts/d859-it-outage-replay.json`)

The replay read corpus headlines from 2010-03-02 to 2026-11-16, 200 months:
- 887 headlines match the terms;
- 304 of them also name a vendor;
- 302 are counted, after 2 denials move to reverse.

Episodes for each floor:

| Floor | Episodes | Per month | Busiest full year |
|---|---|---|---|
| **2 (chosen)** | 40 | 0.20 | 15 |
| 3 | 23 | 0.11 | 9 |
| 4 | 12 | 0.06 | 7 |

Floor 2's episodes include, by eye:
- Delta 2016-08-08;
- AWS 2017-03-01, 2021-12-07 and 2025-10-20;
- the FAA NOTAM failure 2023-01-11;
- CrowdStrike 2024-07-19 (peak 23);
- Alaska 2025-10-24;
- Azure Front Door 2025-10-29;
- Cloudflare 2025-11-18;
- this week's M365 outage and FAA ground stop, 2026-11-12, 74 h, peak 20.

The CrowdStrike aftermath also counts: 2024-07-22 → 09-10, nine episodes on lawsuits and hearings. A follow-up headline that names the vendor and the outage counts as the event's news. That is the burst's known cost.

## The two archive switches

- **`IT-OUTAGE-status-major`** (`new_item`). It reads the four vendors whose stored bytes carry a level:
  - Cloudflare's summary: an unresolved incident's `impact`, `major` or `critical`;
  - Google Cloud: an open incident at `severity` high or `SERVICE_OUTAGE`;
  - AWS: `status` 3, the dashboard's service disruption;
  - Azure: every RSS item, since its public page posts only incidents of wide impact.

  An incident rings once, when it first reaches that level. A stored 200 page that does not read is skipped. The first evaluation seeds, so there is no backlog. AWS's me-central-1 and me-south-1 "Region Availability" events sit at status 3 in today's archive, so they are held and never ring.
- **No level for four vendors.** The history feeds of GitHub, Anthropic, Alpaca and Databento carry no level, and their robots files close the API that would. So no status card names one of the platform's own vendors. The spec's own-exposure line has nothing to say until a level source exists. Their outages still reach the burst through `news.vendors`.
- **`IT-OUTAGE-faa-ground-stop`** (band at 3). It counts the airports of the FAA's Core 30 (aspm.faa.gov, read 2026-11-15) that appear in the newest NAS payload's `Ground_Stop_List`.
  - The archive has held only local stops so far: AUS, SFO, DAL and MCO on 11-15, never more than one of the Core 30 at once.
  - How the feed lists a nationwide stop is not yet seen. The 11-13 stop predates the archive. If it is one program with no airport list, this switch misses it, and the burst caught 11-13 instead.

## Cloudflare Radar — not built

Radar's API asks for a token on every request. Cloudflare's "first request" page says: "To make your first request to Cloudflare's Radar API, you must obtain your API token first." The item's fence makes a key an inbox block, so the block asks for it (`govern/operator-inbox.md`). No Radar request was made.

## The drill (`govern/chokepoints/drills/it-outage-2026-11-15.json`)

The drill ran on a `.backup` copy, reading the archive in place, and passed 10/10:
- every other entry's 2,004 settled hours read as before;
- `it-outage` counted 98 headlines over 167 hours;
- the three switches evaluate:
  - status-major QUIET;
  - news-burst BURST, 7 headlines in 24 h against a bar of 2 (this week's aftermath);
  - ground-stop `<3`.

A first sight is a seed, so the restart pushes nothing.

The walk over the archive found two BLIND spells, both from the archive's start:
- AWS's only row before 23:00Z was D855's probe read (`status_pages#37`, 17:01Z), and it aged past 130 minutes at 19:15Z (D857 (a)'s hourly reads start at #139);
- the FAA had one 33-minute gap in its first hour.
