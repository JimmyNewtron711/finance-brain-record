# Receipt: the bond-ETF NAV arena's papers for the operator's sitting of 2026-11-14 (D843)

**Written** 2026-11-13 ~21:20 ET by the headless `/resume P1` sitting on the checkout `feature/fx-spot-proposer-1`, for D844.

**Why.** The operator answered in chat, 2026-11-13 ~20:43 ET: "Yes they should go on tomorrow's list".

**What this sitting read.**
- Held files and the ledgers.
- Five pages through `rawFetch`: robots and terms only, listed in § 2.
- No NAV export, no ingest, no probe, no Stage-1 receipt, no charter, no spec or K1 edit, and no queue cell.
- The figures in § 4 are arithmetic for the decision. They are not a receipt: the row's `route` is untouched.

**Scratch.** `.review-scratch/d843/` (`fills.mjs`, `get.mjs`).

## 1. The arena rule as written, and the 11-11 line (a)

- **The rule.** Successor Amendment 2026-09-11 (K1) (2), with hypothesis-engine spec § L (2):
  - the source is "the iShares product-page daily NAV history export for `LQD HYG EMB` … URL verified with one request at
    that sitting, fail-closed";
  - TLT and IEF are excluded (Pet17: Treasury ETFs' premium volatility is 10–20 bp, against 50–160 bp for corporate and
    EM);
  - the claim is on ETF **price** returns after a peer-relative deviation;
  - NAV staleness is the registered adverse mechanism (BIS21);
  - Petajisto's before-cost Sharpe of 5 is "a ceiling, never a prior";
  - the class is `sceptical`, and the wallet cell is `y`;
  - "a source is ingested only in the sitting that charters the first family on it".
- **The factory's order.** A new arena is an operator sitting (§ 2.2 condition 2, D33).
  - Before any charter, condition 7's probe reads "on a throwaway scratch pull through `rawFetch`".
  - The production ingest, the module, the tests and the pins come only after the probe.
  - So the probe's pull is the first request to the export, and the rule's one-request URL check can be that request.
- **The 11-11 line does not move the ingest.**
  - Its (6) keeps "each earlier line's terms for its own source", and this source entered by the 09-11 line.
  - Its `admitted:` route token (D841) earns a probe only for a source admitted under 11-11.
  - And its (4) would strike this source on its own terms ("terms that forbid storage or AI use"), because of the
    "intelligent agent" clause quoted in § 2.
- **The row is no factory candidate today**, on three counts: `data` reads `FREE`, the route has no `held:` or
  `admitted:` token, and the route's words "waits for arena" match `NOT_CHARTERABLE`.

## 2. The export's terms, as read (b)

**Pages read** 2026-11-13 ~20:57 ET (robots first; each answered 200):

| depot | id | page | why |
|---|---|---|---|
| `ishares` | 1 | `https://www.ishares.com/robots.txt` | robots |
| `ishares` | 2 | `/us/library/financial-legal-tax` | its legal footer's "Terms & Conditions" link |
| `blackrock` | 1, 2 | `https://www.blackrock.com/robots.txt` | robots; read twice by one script slip, both rows stand |
| `blackrock` | 3 | `/corporate/compliance/terms-and-conditions` | the terms; sha256 `d092bbb1…0fca1e`, 52,338 bytes |

**robots.**
- Both hosts close every path to `Brightbot 1.0` alone.
- For `*` they close only `/*.dl$`, the sign-on paths, `/search/` and the `?truepdf` / `?norepdf` queries. blackrock.com
  also closes `/compliance/`, which is not the terms' path.
- Neither file names a ClaudeBot, anthropic or other AI agent.

**The terms.** ishares.com has no page of its own: its footer links blackrock.com's terms, whose text names
"www.blackrock.com". Verbatim:
- "Such content is solely for your personal, non-commercial use. … You may download material displayed on this Website for
  your personal use provided you also retain all copyright and other proprietary notices … You may not distribute, modify,
  transmit, reuse, repost, or use the content of this Website for public or commercial purposes … without BlackRock's
  written permission."
- Prohibited: "Use any robot, spider, intelligent agent, other automatic device, or manual process to search, monitor or
  copy this Website or the reports, data, information … without BlackRock's permission, provided that generally available
  third-party web browsers may be used without such permission".
- The terms are governed by New York law.

**Not read.** The library page also links an "iShares ETF FDF Terms of Use" PDF, for the fund-data-file service at
`filetransfer.blackrock.com`, a separate channel.

**What binds.** The operator's 10-10 gathering ruling (`6f141065`) covers this: "we can do automated gathering because we
are just using it for personal private non-commercial use". A site's terms against automated gathering do not stop a read
for this platform. Its limits are a refusal addressed to the session, a robots file closed to every agent, a challenge, a
login or a paywall, and none is met here.

**Decision A — how the NAV is read.**
- **(A1)** By script through `rawFetch`, under the 10-10 ruling.
  - Values stay in the depot and git-ignored data.
  - Receipts and the public forward record quote aggregates alone, and nothing is redistributed. This follows the terms'
    distribution bar, in 11-11 (4)'s form.
  - A refusal, a challenge, a login or a payload that is not a NAV history ends the read, with no retry.
- **(A2)** The operator downloads each fund's file by hand in a browser, under the terms' browser proviso, and a session
  records the bytes by `recordRaw`. Every later refresh is by hand too.
- **(A3)** No read without BlackRock's written permission. Asking is the operator's; a session never contacts a vendor.
  The arena waits.
- **Recommended: (A1).** The 10-10 ruling was made for exactly this, robots is open, and the probe is one read per fund.
  The one tension is wording: "intelligent agent" against 11-11 (4)'s "AI use". 11-11 does not govern this source, but
  the line is yours to read.

## 3. The measured cost for these names, against 10 bp/side at h = 5 (c)

**Under the 11-13 cost line (2)**, the probe charges "the arena's measured line where it has one, else the row's declared
cost (10 bp/side by default) times the probe's measured turnover". This arena has no measured line:

| held | names | figure | for LQD HYG EMB |
|---|---|---|---|
| `fill-spread-tlt-2026-10-05.json` | TLT, SIP, 20 sessions, the 15:30 / 16:00 ET fills | median 0.62 bp/side (p75 0.63) | an excluded name, and the most liquid |
| `spread-sample-2026-09-12.json` | 50 S&P 500 stocks | median 4.19, p75 6.54 bp | not these names |
| Alpaca paper fills (`wallet_fills`, `ladder.js` `cost()`'s formula) | `cand-trend-1`'s three sells at the open, 2026-11-03 | EMB 1.69, HYG 5.13, LQD 4.50; mean 3.77 bp/side, n 3 | under `MIN_COST_FILLS` 20, one day, open auction only |

**At the default**, h = 5 is 50.4 rebalances a year. 10 bp/side × turnover T × 50.4 comes to **5.04 % a year per unit of
one-way turnover**:
- T = 0.5 costs 2.5 %;
- T = 1 costs 5.0 %;
- T = 2 (a full flip each week) costs 10.1 %, the whole of Petajisto's 10.63 %/yr before-cost L/S ceiling.

**Decision C — the cost line.**
- **(C1)** Measure first. `node scripts/measure-spread.mjs --fills <SYM>` for each name (Alpaca SIP quotes, the key
  already in `.env`, $0, 40 requests a name, written to `fill-spread-<sym>-<date>.json`). The arena's line is the mean of
  the names' p75 (B1 (5)'s pessimistic end). It is fixed before the probe reads any σ: a cost-only read, not a counted
  trial (D830 (a)'s form).
- **(C2)** The default 10 bp/side × the probe's turnover.
- **Recommended: (C1).** TLT's 0.62 bp suggests 10 bp overstates these names several times over, but only a measurement
  says so, and it has to be taken before the probe to stay honest.

## 4. The Stage-1 re-read owed: form, window and α (d)

**The receipts so far.**
- **2026-09-12:** `ic`, n 2,600, h 5, σ 0.3 declared, α 0.05, prior 0.03 rank IC, P(PASS) 0.63. It predates the ledger,
  the measured-σ rule (10-04) and the cost line (11-13).
- **Megareview 04-eligibility (10-03):** 0.396 at α₁ 0.010937, and 0.265 at α₁ ÷ 3.
- All three figures reproduce as Φ(prior ÷ σ × √(n ÷ h) − z₁₋α/₂): 0.626, 0.396 and 0.265.

**Today.**
- `alpha-wealth --next`: t 3, α_t 0.005494.
- `--cut bond-etf-nav-reversion`: α_member 0.005494 (1 member, 0 probes), and 0.002747 once a probe counts.
- On the declared σ 0.3 the row reads **0.31**, and **0.24** after a probe. That is under the floor, but on a declared σ,
  so it is the probe path and not a kill (10-03 (3) (ii)).

**The fact that decides it: σ is not free here.**
- A rank IC over N names has null variance 1 ÷ (N − 1).
- Over three names, Spearman's ρ takes only −1, −½, ½ and 1, with weights 1/6, 1/3, 1/3 and 1/6, so its null σ is exactly
  **0.707**, not the declared 0.3. Any small true IC leaves it there.
- At σ 0.707 the row reads **0.035** at α_t and **0.021** at α_t ÷ 2. A probe on LQD, HYG and EMB would spend a counted
  trial to book DEAD-POWER.
- With σ = 1 ÷ √(N − 1), prior 0.03, n 2,600, h 5 and α 0.002747, the floor of 0.50 needs about **20 names**:

  | N | 3 | 5 | 8 | 12 | 16 | 20 | 24 | 30 |
  |---|---|---|---|---|---|---|---|---|
  | P(PASS) | 0.02 | 0.05 | 0.12 | 0.23 | 0.37 | 0.50 | 0.61 | 0.76 |

- These are upper bounds: `era_sign` and `plateau_sign` are ignored.

**Decision E — the arena's first family.**
- **(E1)** As written: LQD HYG EMB, the probe in D's form. The expected outcome is DEAD-POWER after one counted trial.
- **(E2)** No probe. The row books DEAD-POWER on its exact three-name σ.
  - This needs your word that a σ fixed by the cross-section's size counts as measured under 10-03 (3) (ii). It is not a
    guess.
  - No trial and no fetch, and the arena stays open with nothing chartered.
- **(E3)** Widen the names by K1 sub-entry, with (E2) for the parent.
  - The names: every iShares US-listed fixed-income ETF in Pet17's corporate, high-yield, EM and municipal groups with a
    NAV history from on or before 2015-12-31. Treasury-only funds stay out.
  - The list is drawn by that rule from the iShares product list, then committed and mirror-pushed before any NAV read.
  - A new row, `bond-etf-nav-reversion-wide` (the parent's X, its own Stage 1 at σ 1 ÷ √(N − 1)), enters before any read.
  - Pet17's peer-relative L/S ranked many ETFs against their category peers, not three names, so this is nearer the
    paper.
  - The cost: one NAV file a fund under (A); price history from Sharadar `funds` up to 2015-12-31 (held); and Alpaca bars
    from 2016 for names outside `equity_daily_tr`'s 22 (free, an ingest). The wallet cell is `n` for non-roster names, so
    the family is research-only.
- **Recommended: (E3).** It is the build the operator's lines favour ("Adapt every paper hypothesis", "build over
  closing"), and the only version whose own arithmetic can clear. With no answer, (E1) stands: the arena as written.

**Decision D — the probe, under (E1) or (E3).**
- **D1, the form.**
  - (i) D533 (b)'s σ-only probe: σ_IC, the L/S expression's σ_gross and σ_net, its turnover and its cost. No mean and no
    `clears`. One counted trial, by a script committed and mirror-pushed before its one read.
  - (ii) Condition 7's full probe: the IC's mean as well and `clears`. A non-clearing probe books DEAD-PROBE.
  - Recommended (i): no mean is read before the pre-registered evaluation.
- **D2, the window.**
  - (i) Discovery 2008-01-02 → 2015-12-31, and confirmation 2016-01-04 → (about 2,730 sessions, against the declared
    2,600).
    - EMB's first `funds` bar is 2007-12-19 (`sharadar-funds-basis-2026-11-02.md`), so 2008 is the first full year with
      prices for all three names. The NAV history's start is known only once it is read.
    - The split sits on the price tape's own seam: Sharadar `funds` up to 2015, then Alpaca TR `equity_daily_tr`, both
      held for all three names.
    - It keeps March 2020, BIS21's adverse episode, out of sample.
  - (ii) Discovery 2008 → 2012, Pet17's era plus two years, and confirmation 2013 →.
  - (iii) No split: the probe reads the whole history, and the evaluation is forward-only.
  - Recommended (i).
- **D3, α.**
  - (i) One member, the pooled rank IC: α_t ÷ (1 + probes), read by `alpha-wealth --cut` at the charter (0.002747 at
    t 3).
  - (ii) Three members, one a name: 0.001374.
  - Recommended (i): the statistic is one cross-section.
- **D4, the mean-form prior.** The 11-13 line (3) says that for an `ic` row "the charter's re-check runs in the `mean`
  form, on that expression's measured σ and net prior". The row has no mean-form prior.
  - (i) Carry the IC prior into return units by the measured cross-sectional dispersion (Grinold's bridge), net of the
    cost.
  - (ii) Use the row's haircut cell, E[SR] ≤ 0.3 before costs. σ then cancels: over ~10.8 confirmation years the expected
    t is 0.3 × √10.8 ≈ 0.99 against z 2.99, so no version clears whatever N or σ.
  - Recommended (i). The cell was written for three names: 0.03 × √(3 × 50.4) ≈ 0.37. Under (E3) it is re-declared from
    N.

## 5. The arena's other rows (e)

| row | status | last Stage 1 | what it needs |
|---|---|---|---|
| `bond-etf-nav-reversion` | `QUEUED` | 0.63, α 0.05, declared σ (09-12) | this paper |
| `bond-etf-overnight-overshoot` | `QUEUED` | 0.05 at α 0.01094 on a declared σ, probe path (10-04) | n 2 events on the held tape (LQD 2008-09-30, HYG 2020-04-09); NAV only an integrity diagnostic |
| `lqd-accepted-basket-unwind` (novel, gen A) | `QUEUED` | 0.05 at α 0.01094 on a declared σ, probe path (10-04) | "timestamped shares-outstanding history must be present in the issuer download or no charter"; whether the export carries it is unknown until it is read |

- **The catalogue** holds 65 entries in arena `bond-etf-nav`: these 3 queue rows, 60 `sweep-bond-etf-nav` and 2
  `sweep-treasuries`. None is a queue row or a claim.
- **Recommended:** neither other row joins the first family. Each keeps its own probe path, and the export's columns,
  once read, answer the basket row's condition.

## 6. Drafted dated sub-entry, on the recommended options, for approval in Saturday's chat

> **2026-11-14 (K1, dated line under Amendment 2026-09-11 (K1) (2), bond-ETF NAV) — the arena's first family: its read,
> its names, its cost line and its probe.** Written by the monitor session on the operator's chat approval of this exact
> text, drafted from `govern/receipts/bond-etf-arena-papers-2026-11-14.md`. Approved 2026-11-14 ~HH:MM ET, verbatim:
> "<…>". In force at the commit that carries it, mirror-pushed before any read under it.
> - (1) **The read (A1).** The iShares product-page NAV history export is read by script through `rawFetch` under the
>   10-10 gathering ruling (`6f141065`). The site's terms (depot `blackrock` id 3, read 2026-11-13) limit it to personal,
>   non-commercial use. Values stay in the depot and git-ignored data. Receipts and the public forward record quote
>   aggregates alone, and nothing is redistributed. A refusal, challenge, login or non-NAV payload ends the read, with no
>   retry.
> - (2) **The names (E3).** The arena's names become every iShares US-listed fixed-income ETF in Pet17's corporate,
>   high-yield, EM and municipal groups whose NAV history starts on or before 2015-12-31. Treasury-only funds stay out.
>   - The list is drawn by that rule from the iShares product list. It is committed and mirror-pushed before any NAV read.
>   - `bond-etf-nav-reversion-wide` enters the queue with the parent's X, form `ic`, h 5, prior 0.03 rank IC and σ
>     1 ÷ √(N − 1) at its N, at the ledger's α, before any read.
>   - `bond-etf-nav-reversion` books DEAD-POWER on its exact three-name σ 0.707 (P(PASS) 0.02 at α 0.002747). A σ fixed
>     by the cross-section's size is a measured σ for Amendment 2026-10-03 (K1) (3) (ii).
>   - The family is research-only (wallet `n` off the roster).
> - (3) **The ingest.** The probe's scratch pull (factory spec § 2.2 condition 7) is the first read, one request a fund,
>   and it is the URL check, fail-closed. The production ingest waits for the charter, as (2) writes it. The 11-11 line
>   does not reach this source (its (6)).
> - (4) **The cost line (C1).** Before the probe, `measure-spread.mjs --fills` reads each name. The arena's line is the
>   mean of the names' p75: a cost-only read, not a counted trial. Absent it, the 10 bp/side default × the probe's
>   turnover.
> - (5) **The probe (D1 (i), D2 (i)).** D533 (b)'s σ-only probe, once, on discovery 2008-01-02 → 2015-12-31.
>   - It reads σ_IC, the L/S expression's σ_gross and σ_net, its turnover and its cost. It reads no mean and no `clears`.
>   - It is one counted trial, by a script committed and mirror-pushed before its one read.
>   - Then Stage 1 re-runs at the measured σ and the net prior. The mean form's prior is the IC prior carried by the
>     measured cross-sectional dispersion (D4 (i)).
>   - Confirmation (2016-01-04 →) is read once, by `factory-evaluate`.
> - (6) **α (D3 (i)).** One member: α_member = α_t ÷ (1 + probes), by `alpha-wealth --cut` at the charter.
> - (7) **Not changed:** the other two arenas of 2026-09-11 (2); TLT and IEF's exclusion; NAV staleness as the adverse
>   mechanism; class `sceptical`; Pet17's ceiling never a prior; the 0.50 floor, the ½ haircut and the cost line of
>   2026-11-13; `bond-etf-overnight-overshoot` and `lqd-accepted-basket-unwind`; K2 and § 5; and every frozen
>   pre-registration.

**Swaps for other answers.**
- (E1): (2) reads "The names stay `LQD HYG EMB`", the new row and the DEAD-POWER sentence drop out, and (5)'s probe runs
  on the parent.
- (E2) alone: (2)'s DEAD-POWER sentence stays, and (3) to (6) drop out.
- (A2): (1) reads "by hand in a browser by the operator, the bytes recorded by `recordRaw`".
- (C2): (4) reads "the 10 bp/side default × the probe's turnover".
