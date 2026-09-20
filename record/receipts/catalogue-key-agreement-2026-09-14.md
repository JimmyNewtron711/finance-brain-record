# Catalogue key agreement — 2026-09-14 (spec 2026-09-14-novel-hypothesis-lane-design.md §2.3; plan Task 5)

Bar: full four-token key agreement ≥ 90 % on a 50-entry blind sample (`node scripts/catalogue.mjs sample --n 50 --seed <s>`; the re-keyer sees id, title, source and x_detail only). Most Task 3 batches were keyed on lane A (sonnet), so each scored re-key comes from another lane.

## Round 0 — seed 0

- Catalogue: 2023 entries at `282ddea5` (Task 4 commit).
- Re-key: duel 481 (bulk-extraction, silent). Scored side = codex gpt-6-astra@high (the route pick; lane ≠ lane A). Brief `.review-scratch/duel481-brief.md` = keying-brief.md with the sample as INPUT and the plan's added line.
- `node scripts/catalogue.mjs agree govern/catalogue/strategies.jsonl .review-scratch/catalogue/keyed/agree-0.jsonl` (scored file = the codex side's output), verbatim:

```
agreement: 21/50 = 42.0 %
  hlz:sharpe--1964-: volatility/us-equity-xs/le1m/pit-sp500 vs volatility/us-equity-index/le1m/pit-sp500
  hlz:edmans--2011-: intangibles/us-equity-xs/gt1m/pit-sp500 vs intangibles/us-equity-xs/le1m/pit-sp500
  osap:assetturnover: profitability/us-equity-xs/gt1m/pit-sp500 vs profitability/us-equity-xs/le1m/pit-sp500
  sweep-bond-etf-nav:em-credit-factors: size/bond-etf/le1m/bond-etf-nav vs size/bond-etf/le1m/outside
  sweep-bond-etf-nav:credit-derivative-relative-value: basis/bond-etf/le5d/bond-etf-nav vs basis/bond-etf/le1m/bond-etf-nav
  qp:-0102: seasonality/us-equity-index/le5d/pit-sp500 vs seasonality/us-equity-xs/le5d/pit-sp500
  hxz:ig: investment/us-equity-xs/gt1m/pit-sp500 vs investment/us-equity-xs/le1m/pit-sp500
  osap:chforecastaccrual: profitability/us-equity-xs/gt1m/pit-sp500 vs quality/us-equity-xs/le1m/pit-sp500
  sweep-crypto-micro:funding-rate-granger-trend-signal: funding/btc-eth-perp/le5d/crypto-micro vs funding/btc-eth-perp/le1m/crypto-micro
  sweep-microcap:otc-momentum-weak: momentum/us-microcap-xs/gt1m/microcap vs momentum/us-equity-xs/le1m/pit-sp500
  sweep-bond-etf-nav:gamma-imbalance-eod-pressure: inventory/etf-options/intraday/options vs inventory/us-equity-index/intraday/pit-sp500
  qp:-0031: seasonality/us-equity-index/gt1m/pit-sp500 vs seasonality/global-equity-xs/gt1m/outside
  sweep-microcap:buyback-drift-small-value: investment/us-microcap-xs/gt1m/microcap vs announcement/us-microcap-xs/gt1m/microcap
  sweep-fx-spot:value-reversal: reversal/fx-majors/le1m/fx-spot vs value/fx-majors/le1m/fx-spot
  osap:capturnover: profitability/us-equity-xs/gt1m/pit-sp500 vs profitability/us-equity-xs/le1m/pit-sp500
  osap:rio_mb: dispersion/us-equity-xs/le1m/pit-sp500 vs value/us-equity-xs/le1m/pit-sp500
  hlz:row-243: quality/us-equity-xs/le1m/pit-sp500 vs quality/global-equity-xs/le1m/outside
  osap:pm: profitability/us-equity-xs/gt1m/pit-sp500 vs profitability/us-equity-xs/le1m/pit-sp500
  hlz:fung-and-hsieh--2001-: momentum/us-equity-xs/le1m/pit-sp500 vs volatility/etf-options/le1m/options
  hxz:dwc: quality/us-equity-xs/gt1m/pit-sp500 vs investment/us-equity-xs/le1m/pit-sp500
  hlz:bazdresch--belo-and-lin--2012-: investment/us-equity-xs/gt1m/pit-sp500 vs investment/us-equity-xs/le1m/pit-sp500
  sweep-microcap:ivol-puzzle: volatility/us-microcap-xs/le1m/microcap vs volatility/us-equity-xs/le1m/pit-sp500
  osap:hire: investment/us-equity-xs/gt1m/pit-sp500 vs investment/us-equity-xs/le1m/pit-sp500
  sweep-crypto-micro:synthetic-futures: liquidity/btc-eth-options/le1m/crypto-micro vs basis/btc-eth-options/le1m/crypto-micro
  sweep-treasuries:mbs-convexity-hedging-flows: flow-event/ust-futures/le1m/treasuries vs inventory/ust-futures/le1m/treasuries
  osap:netdebtprice_q: quality/us-equity-xs/gt1m/pit-sp500 vs value/us-equity-xs/le1m/pit-sp500
  osap:tax_q: quality/us-equity-xs/gt1m/pit-sp500 vs quality/us-equity-xs/le1m/pit-sp500
  queue:sp500-beta-constraint: quality/us-equity-xs/le1m/pit-sp500 vs volatility/us-equity-xs/le1m/pit-sp500
  osap:bm: value/us-equity-xs/gt1m/pit-sp500 vs value/us-equity-xs/le1m/pit-sp500
```

- For information (not scored): the lane-A sonnet side of the same duel scored `agreement: 22/50 = 44.0 %` against the catalogue, and the two blind re-keys agreed with each other `agreement: 32/50 = 64.0 %` — the spread is in the definitions, not one lane.

### Changes between round 0 and round 1

Of the 29 disagreements: 11 differ only in `horizon` (mostly `gt1m` vs `le1m` on monthly-rebalanced accounting anomalies; two `le5d` vs `le1m`), 7 only in `object` / `arena` (index vs cross-section, a restricted or non-US universe, an arena chosen apart from its object), 6 only in `x_family`, 5 on several tokens. No token was added. `govern/catalogue/keying-brief.md` gained a KEYING RULES section: (1) object = the instrument whose return is traded or predicted, with the index / cross-section / micro-cap / global tests; (2) arena follows object through a fixed map; (3) a horizon precedence — printed holding period, printed rebalance interval, cross-sectional anomaly sorts default `le1m`, else observation frequency; (4) x_family tie-breaks for the confused pairs (profitability / value / quality, beta → volatility, investment vs announcement drift, reversal vs value, inventory vs flow-event, basis, intangibles). Because rules 2–3 touch most of the 2023 entries (719 carried `gt1m`), every entry was re-keyed from the same four texts the agreement sample shows (id, title, source, x_detail) under the new rules — duel 482 on chunk 01, codex gpt-6-astra@high on chunks 02–12 — and the keys merged back into `strategies.jsonl` (titles, sources, x_detail and reported_stat unchanged).

## Round 1 — seed 1

- Catalogue: 2023 entries after the round-1 re-key (keys changed on 1150 entries; `build` rc 0; tests 40 passed). Catalogue keying lane this round = codex gpt-6-astra@high (duel 482 chunk 01 + chunks 02–12).
- Re-key: duel 483 (bulk-extraction, silent; route pick codex). Scored side = lane A sonnet (lane ≠ the catalogue's keying lane), brief `.review-scratch/duel483-brief.md` (seed-1 sample, KEYING RULES applied).
- `node scripts/catalogue.mjs agree govern/catalogue/strategies.jsonl .review-scratch/catalogue/keyed/agree-1.jsonl` (scored file = the lane-A side's output), verbatim:

```
agreement: 34/50 = 68.0 %
  sweep-treasuries:macro-forecast-disagreement: dispersion/ust-futures/le1m/treasuries vs announcement/ust-futures/intraday/treasuries
  sweep-treasuries:delta-hedged-option-returns: volatility/etf-options/le1m/outside vs volatility/ust-futures/le1m/treasuries
  sweep-crypto-micro:cross-venue-funding: funding/btc-eth-perp/le1m/crypto-micro vs funding/btc-eth-perp/intraday/crypto-micro
  sweep-treasuries:short-basis: basis/ust-futures/le1m/treasuries vs basis/ust-futures/gt1m/treasuries
  queue:treasury-borrowing-release: announcement/ust-etf/le5d/treasuries vs flow-event/ust-etf/le5d/treasuries
  sweep-fx-spot:day-of-month-momentum-seasonality: seasonality/fx-majors/le5d/fx-spot vs seasonality/fx-majors/le1m/fx-spot
  hlz:chordia--subrahmanyam-and-tong--2013-: value/us-equity-xs/le1m/pit-sp500 vs quality/us-equity-xs/le1m/pit-sp500
  osap:exchswitch: announcement/us-equity-xs/le1m/pit-sp500 vs liquidity/us-equity-xs/le1m/pit-sp500
  hlz:pieter--lo-and-pfeiffer--2011-: profitability/us-equity-xs/le1m/pit-sp500 vs announcement/us-equity-xs/le1m/pit-sp500
  sweep-crypto-micro:random-maturity-arbitrage-perp: basis/btc-eth-perp/le1m/crypto-micro vs basis/btc-eth-perp/intraday/crypto-micro
  osap:betacr: volatility/us-equity-xs/le1m/pit-sp500 vs liquidity/us-equity-xs/le1m/pit-sp500
  sweep-crypto-micro:cross-impact-taker: lead-lag/btc-eth-perp/intraday/outside vs lead-lag/btc-eth-perp/intraday/crypto-micro
  osap:noa: quality/us-equity-xs/le1m/pit-sp500 vs investment/us-equity-xs/le1m/pit-sp500
  sweep-treasuries:maturity-extension-program: flow-event/ust-futures/le1m/treasuries vs term-structure/ust-etf/gt1m/treasuries
  sweep-crypto-micro:btc-eth-cointegration: reversal/btc-eth-perp/le1m/outside vs reversal/btc-eth-perp/le5d/crypto-micro
  sweep-bond-etf-nav:mp-shock-loan-fund-flow-asymmetry: announcement/bond-etf/le1m/outside vs flow-event/bond-etf/le1m/outside
```

- For information (not scored): the codex side of duel 483 — the same lane as the catalogue keying — scored `agreement: 41/50 = 82.0 %`.

### Changes between round 1 and round 2

Of the 16 disagreements: 8 differ in `x_family` where two families fit the text (announcement vs flow-event / profitability / liquidity / dispersion, quality vs investment / value, volatility vs liquidity, flow-event vs term-structure), 6 in `horizon` on non-stock signals (sub-daily funding and basis, event windows, a day-of-month effect), 3 in `arena` through rule 2's `outside` clause (crypto pairs, bond-fund flows) and 2 in `object` (options on Treasuries, cash vs futures). Changes: rule 1 now maps any-coin crypto perps/options and options on Treasuries; rule 2's `outside` clause lists exactly which instruments qualify; rule 3 gained an event-window clause and a many-asset sort default, and names sub-daily updates `intraday`; new rule 5 is a strict `x_family` precedence order for signals that still fit two families; one token added — `macro-beta` (macro and consumption risk exposures, which the duel-482 re-key side reported it had been forcing into `volatility`), added to `VOCAB` in `scripts/catalogue.mjs` and to the keying brief's VOCABULARY. The catalogue was re-keyed again from the same four texts (duel 484 on chunk 01, codex gpt-6-astra@high on chunks 02–12).

## Round 2 — seed 2

- Catalogue: 2023 entries after the round-2 re-key (keys changed on 539 entries vs round 1; `build` rc 0; tests 40 passed). Catalogue keying lane = codex gpt-6-astra@high (duel 484 chunk 01 + chunks 02–12).
- Re-key: duel 485 (bulk-extraction, silent; route pick codex). Scored side = lane A sonnet, brief `.review-scratch/duel485-brief.md` (seed-2 sample, KEYING RULES 1–5).
- `node scripts/catalogue.mjs agree govern/catalogue/strategies.jsonl .review-scratch/catalogue/keyed/agree-2.jsonl` (scored file = the lane-A side's output), verbatim:

```
agreement: 37/50 = 74.0 %
  hxz:fq1: profitability/us-equity-xs/le1m/pit-sp500 vs quality/us-equity-xs/le1m/pit-sp500
  sweep-bond-etf-nav:hy-200dma-switch: momentum/bond-etf/le5d/outside vs momentum/bond-etf/le5d/bond-etf-nav
  queue:treasury-auction-cycle: flow-event/ust-etf/le1m/treasuries vs flow-event/ust-etf/le5d/treasuries
  hlz:guo-and-savickas--2008-: volatility/global-equity-xs/le1m/outside vs volatility/us-equity-xs/le1m/pit-sp500
  queue:timesfm-wm2ns-forward: macro-beta/us-equity-index/le1m/pit-sp500 vs macro-beta/ust-etf/le1m/treasuries
  sweep-options:delta-hedging-cost: liquidity/etf-options/le1m/options vs inventory/etf-options/le1m/options
  osap:ms: profitability/us-equity-xs/le1m/pit-sp500 vs quality/us-equity-xs/le1m/pit-sp500
  sweep-bond-etf-nav:cp-forward-rate-factor: term-structure/ust-futures/gt1m/treasuries vs term-structure/ust-etf/gt1m/treasuries
  hxz:ala: liquidity/us-equity-xs/gt1m/pit-sp500 vs quality/us-equity-xs/gt1m/pit-sp500
  osap:opleverage_q: quality/us-equity-xs/le1m/pit-sp500 vs profitability/us-equity-xs/le1m/pit-sp500
  sweep-treasuries:ctd-switch-delivery-option: basis/ust-futures/le1m/treasuries vs basis/ust-futures/gt1m/treasuries
  hlz:lintner-1965-: volatility/us-equity-xs/le1m/pit-sp500 vs macro-beta/us-equity-xs/le1m/pit-sp500
  sweep-microcap:social-media-manipulation: text-sentiment/us-microcap-xs/le1m/microcap vs text-sentiment/us-microcap-xs/le5d/microcap
```

- For information (not scored): the codex side of duel 485 scored `agreement: 39/50 = 78.0 %`; the two blind sides agreed with each other `agreement: 31/50 = 62.0 %`.

## Verdict — below 90 % after three rounds (plan Task 5 Step 4)

| round | seed | rules | scored lane | agreement | same-lane re-key (info) |
|---|---|---|---|---|---|
| 0 | 0 | vocabulary glosses only | codex | 42.0 % | 44.0 % (lane A vs a mostly lane-A catalogue) |
| 1 | 1 | + KEYING RULES 1–4 | lane A | 68.0 % | 82.0 % (codex) |
| 2 | 2 | + rule 5 precedence, tightened 1–3, token `macro-beta` | lane A | 74.0 % | 78.0 % (codex) |

The catalogue is valid (2023 entries) but its keys do not reach the ≥ 90 % receipt the novelty gate requires, so Tasks 6–7 are parked and an inbox block asks the operator how to proceed. In round 2 the 13 misses are 6 `x_family` (profitability / quality / liquidity pairs on accounting signals, volatility vs macro-beta on CAPM-type factors, liquidity vs inventory on hedging cost), 3 `horizon`, 4 `object` / `arena` (a US-vs-global sample, bond-ETF arena, an ETF-vs-futures Treasury object, a macro forecast's traded object). Cross-lane agreement has risen with each tightening while same-lane agreement stayed near 80 %, which puts the ceiling in the text the key is read from (id, title, source, x_detail) as much as in the rules.

## Closing note — 2026-09-15 (operator ruling)

The ≥ 90 % bar this receipt was measured against was retired the day after it was written. Operator ruling option (a) on the
inbox block *"2026-09-14 — novel lane: catalogue key agreement below 90 % after three rounds"*, carried as successor-doc
**Sub-entry 2026-09-15 (K1)** and spec §6 P3: the bar is **≥ 70 % on the full four-token key** (round 2's measured **74 %**
clears it), and a key match is demoted to a **lead** — every novel row goes to the blind prior-art hunter regardless, exact ids
included, and a gate run missing a hunter verdict is refused. No fourth re-key round was run: the three rounds in this receipt
are the evidence the bar was set from. Plan Tasks 6–7 unparked.
