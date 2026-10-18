# Shadow books — borrow line and the lines before the first mark (2026-10-17, D137)

**Books:** `tsmom-bridge` (`lb9`), `tsmom-bridge-etf2` (`lb12`), `carry-basis-cs-tilt` (`s21`), all concluded DIE, all
`status: shadow` on the local sim leg. Authority: the inbox Applied block *"2026-10-03 — Megareview — enable the first
SHADOW book (D86), with a K5 carve-out by name"* (`A: b, all three.`) and Amendment 2026-10-03 (K1), megareview rulings
(1); spec `docs/superpowers/specs/2026-09-15-shadow-books.md`. Written in the operator's interactive sitting of 2026-10-17.
The two TSMOM books pin this file by sha256 in `shadow_borrow_bp_yr`; `carry-basis-cs-tilt` is long-only and pins nothing
here.

## 1. Borrow line — `bp_yr: 0` for `tsmom-bridge` and `tsmom-bridge-etf2`

Both weights files carry `constraints.long_only: false` and neither envelope states `inputs.costs.borrow_bp_yr`, so the
loader needs the line from the book (spec § 2). The number is **0 bp/yr**: Alpaca charges $0 locate and borrow on
easy-to-borrow shares; hard-to-borrow is live-only (alpaca.markets/support/short-selling-fees, read 2026-10-02 — the same
line as `govern/receipts/subset-price-2026-10-02.json` `borrow`). The sim leg never charges borrow; the line exists so the
number is written down. It is a declared line, not an observation.

Per-symbol flags from Alpaca's paper assets list as stored in the raw depot — `data/raw/alpaca/payloads.db` id 82208,
`GET /v2/assets?asset_class=us_equity&status=active`, fetched 2026-10-02 11:18:58 ET, body sha256
`bec5a575c26f69ebf95588878fea22faf6238459a4b1cc935bb03f981c2fce25` — read through the wallet's own `shortEligible`
(`server/services/wallet/alpaca.js`). No request was made for this receipt.

| symbol | book | shortable | borrow_status | easy_to_borrow | `shortEligible` |
|---|---|---|---|---|---|
| SPY | both | true | easy_to_borrow | true | yes |
| TLT | both | true | easy_to_borrow | true | yes |
| GLD | both | true | easy_to_borrow | true | yes |
| IEF | both | true | easy_to_borrow | true | yes |
| USO | both | false | hard_to_borrow | false | no — not shortable |
| DBA | both | true | easy_to_borrow | true | yes |
| QQQ | etf2 | true | easy_to_borrow | true | yes |
| IWM | etf2 | true | easy_to_borrow | true | yes |
| EFA | etf2 | true | easy_to_borrow | true | yes |
| EEM | etf2 | true | easy_to_borrow | true | yes |
| VNQ | etf2 | true | easy_to_borrow | true | yes |
| TIP | etf2 | true | easy_to_borrow | true | yes |
| LQD | etf2 | true | easy_to_borrow | true | yes |
| HYG | etf2 | true | easy_to_borrow | true | yes |
| EMB | etf2 | true | easy_to_borrow | true | yes |
| SLV | etf2 | true | easy_to_borrow | true | yes |
| DBC | etf2 | true | easy_to_borrow | true | yes |
| UUP | etf2 | true | easy_to_borrow | true | yes |
| FXE | etf2 | false | hard_to_borrow | false | no — not shortable |
| FXY | etf2 | true | easy_to_borrow | true | yes |

**Stated plainly:** USO (both books) and FXE (`tsmom-bridge-etf2`) were not shortable on Alpaca paper on 2026-10-02. A
shadow book's short open asks no broker (`run.js`, Resolution 8), so the sim leg will short them when a row says so; an
Alpaca book would see those legs refused. That is a known difference between the shadow books and any real book, not a
defect to fix in them.

## 2. Before the first mark (synthesis § 3.2 P-B; Amendment 2026-10-03 (K1) (1)) — each book

- Each DIE stays a DIE. No shadow mark re-tests it.
- A variant inspired by a shadow book is a new program id under its own pre-registration.
- No shadow mark is cited as alpha, as forward confirmation or as a criticism of a gate, in any document, case studies
  included.
- A shadow book is never a claim, a verdict, a `claims.json` performance entry or a Forward Record figure, and never
  discharges K3.
- Sim leg only; no Alpaca order of any kind.

**Kill criteria (synthesis § 5, read per book):** fewer than 20 scheduled-session dispositions by 2026-11-13, any
undocumented change to the frozen book, or any document citing its marks as evidence — that book's pilot failed. A kill is
`"status": "killed"`, any session, one commit.
