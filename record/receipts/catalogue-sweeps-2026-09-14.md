# Catalogue arena sweeps — 2026-09-14 (spec 2026-09-14-novel-hypothesis-lane-design.md §2.3 step 3; plan Task 4)

`route_task web-research` routed each arena as a UNION (both sides run, both kept, no judges): side A = lane B opus@high, side B = codex gpt-6-astra@high.
Brief = `govern/catalogue/sweep-brief.md` with the arena filled in. Merge rule: both sides' JSONL concatenated; an entry dropped when an earlier kept entry has the same four-token key AND the same id or a shared source URL; an id collision with a different entry gets `-2`. Forced-actor rows merged, deduplicated by actor name, their catalogue-id cells remapped to kept ids.

| arena | union | side | model | searches run | lines | actors | sub-agents | permission denials |
|---|---|---|---|---|---|---|---|---|
| fx-spot | 475 | A | lane B opus@high | 60 | 64 | 11 | 0 | 8 |
| fx-spot | 475 | B | codex gpt-6-astra@high | 60 | 99 | 6 | 3 | n/a (sandbox) |
| treasuries | 476 | A | lane B opus@high | 112 (disclosed overrun of the ≤ 60 budget, 6 sub-agents) | 98 | 12 | 6 | 0 |
| treasuries | 476 | B | codex gpt-6-astra@high | 60 | 60 | 7 | 3 | n/a (sandbox) |
| options | 477 | A | lane B opus@high | 53 | 77 | 9 | 0 | 3 |
| options | 477 | B | codex gpt-6-astra@high | 60 | 116 | 7 | 3 | n/a (sandbox) |
| crypto-micro | 478 | A | lane B opus@high | 55 | 129 | 10 | 7 | 0 |
| crypto-micro | 478 | B | codex gpt-6-astra@high | 60 | 89 | 10 | 3 | n/a (sandbox) |
| bond-etf-nav | 479 | A | lane B opus@high | 61 (disclosed, 6 sub-agents) | 77 | 15 | 6 | 51 |
| bond-etf-nav | 479 | B | codex gpt-6-astra@high | 60 | 54 | 8 | 3 | n/a (sandbox) |
| microcap | 480 | A | lane B opus@high | 60 | 59 | 11 | 0 | 3 |
| microcap | 480 | B | codex gpt-6-astra@high | 60 | 58 | 8 | 3 | n/a (sandbox) |

## Kept after merge

| arena | lines kept | forced-actor rows |
|---|---|---|
| fx-spot | 128 | 17 |
| treasuries | 144 | 19 |
| options | 155 | 16 |
| crypto-micro | 163 | 20 |
| bond-etf-nav | 115 | 23 |
| microcap | 102 | 19 |
| total | 807 | |

## Source spot-checks (plan Task 4 Step 3: three random lines per arena, each URL opened by the controller)

Result: 20 URLs checked, 0 fabricated or non-matching, 2 access-blocked (SSRN, CME — both returned HTTP 403 to WebFetch and curl) and replaced by a further draw from the same arena. No line deleted; no arena re-dispatched.

### fx-spot

- L15 sweep-fx-spot:currency-value-raw-rer — papers.ssrn.com abstract 2282480: HTTP 403 to WebFetch and curl ("Content Blocked") — UNVERIFIABLE (access-blocked, not judged fabricated); replaced by L24
- L46 sweep-fx-spot:monetary-restrictiveness-signal — nber.org/papers/w33423: MATCH ("The relative restrictiveness of a central bank's supply of money predicts the raw and risk-adjusted returns of its currency")
- L59 sweep-fx-spot:turn-of-month-currencies — cxoadvisory.com turn-of-the-month-effect-for-currencies: MATCH (page investigates the currency turn-of-month effect; findings paywalled)
- L24 sweep-fx-spot:order-flow-exchange-rate — nber.org/papers/w7317: MATCH (Evans & Lyons 1999, "Order Flow and Exchange Rate Dynamics")

### treasuries

- L132 sweep-treasuries:calendar-spreads-with-tails — cmegroup.com education article: WebFetch timeout, curl HTTP 403 — UNVERIFIABLE (access-blocked); replaced by L98
- L71 sweep-treasuries:orderflow-imbalance-yields — Brandt & Kavajecz JF 2004 PDF (pdftotext): MATCH ("orderflow imbalances … account for up to 26% of the day-to-day variation in yields")
- L93 sweep-treasuries:tdf-pension-rebalancing — rpc.cfainstitute.org Enterprising Investor 2025: MATCH ("This exposes them to front-running.")
- L98 sweep-treasuries:equity-tail-risk — arxiv.org/abs/2007.05933: MATCH (Rubin & Ruzzi, "Equity Tail Risk in the Treasury Bond Market")

### options

- L155 sweep-options:collar — optionseducation.org collar page: MATCH
- L142 sweep-options:relative-iv-spx-nya — ideas.repec.org FAJ 58(6): MATCH (Ammann & Herriger 2002, "Relative Implied-Volatility Arbitrage with Index Options")
- L135 sweep-options:overnight-to-overnight-momentum — cfr-cologne.de CFR WP 26-02 (pdftotext): MATCH (Bali, Goyal, Mörke & Weigert, "strong momentum within the same period")

### crypto-micro

- L122 sweep-crypto-micro:minimum-variance-perp-hedge — arxiv.org/abs/2101.01261: MATCH on paper identity (title "Hedging with Bitcoin Futures: The Effect of Liquidation Loss Aversion and Aggressive Trading" = the cited source; the entry keys the paper's benchmark hedge)
- L17 sweep-crypto-micro:btc.termstructure.backwardation-reversion — insights.deribit.com: MATCH ("The mean TTL of Backwardation … is around 85 hours")
- L148 sweep-crypto-micro:dov-auction-prehedge — research.ribbon.finance: MATCH ("market makers … sell the relevant options on exchanges ahead of the auction")

### bond-etf-nav

- L14 sweep-bond-etf-nav:bond-etf-redemption-basket-quality-tilt — bis.org r_qt2103d: MATCH ("bonds in the redemption baskets tend to have shorter duration and slightly lower liquidity")
- L74 sweep-bond-etf-nav:volatility-managed-portfolio — nber.org/papers/w22208: MATCH (Moreira & Muir 2016)
- L78 sweep-bond-etf-nav:msg — arxiv.org/html/2504.06289v1: MATCH (momentum factor on LQD/HYG duration-neutral returns)

### microcap

- L93 sweep-microcap:russell-growth-deletions — link.springer.com 10.1007/s11156-006-7441-3: login redirect; Crossref metadata = Chen (2006) "On Russell index reconstitution", RQFA — MATCH on paper identity
- L80 sweep-microcap:small-ebitda-ev — aaii.com O'Shaughnessy characteristics: MATCH ("Ratio of EBITDA to enterprise value (EV) combined with small stocks")
- L10 sweep-microcap:otc-illiquidity-premium — nber.org/papers/w19309: MATCH (Ang, Shtauber & Tetlock 2013, "the OTC illiquidity premium is several times higher")

## Unsourced lists (copied verbatim from the twelve side reports)

### fx-spot — side A (union 475)

- Triangular arbitrage and cross-venue latency arbitrage (EBS vs Reuters/LSEG) in spot.
- Volatility-scaled ("risk-managed") carry and momentum overlays — scaling the standard carry basket by realised volatility.
- Big Mac / Economist PPP-basket value screens.
- Roll-yield carry implemented through CME listed currency futures rather than forwards.
- Barrier/digital option defence trading — dealers defending a barrier strike into the cut.
- Sovereign wealth fund oil-revenue recycling flows as an FX signal.
- Weekend/Monday and "Turnaround Tuesday" day-of-week effects in spot FX.
- Carry conditioned on VIX or global risk appetite (the "dollar smile" framing).
- CFTC Commitments of Traders positioning signals in currency futures.
- Retail broker positioning (contrarian sentiment) signals.
- NDF fixing and capital-control screens in EM carry baskets.
- Momentum-crash timing / carry-momentum interaction overlays.

### fx-spot — side B (union 475)

- Gotobi (Japanese dates divisible by five), day-of-week, January and generic turn-of-month FX rules: no adequately fetched rule source. Khademalomoom and Narayan (2020), Intraday-of-the-week effects, publisher/DOI opens failed.
- Standalone central-bank intervention trading, and 2022 Global Portfolio Rebalancing and Exchange Rates: source fetch or rule detail insufficient. The older Hau-Rey mechanism is included only through the opened Melvin-Prins paper.
- Bakshi and Panayotov commodity-, volatility- and liquidity-conditioned carry: search abstracts found, attempted SSRN/ScienceDirect/mirror opens failed.
- Crash-neutral carry (Jurek) and separately attributed volatility-targeted carry: necessary source details not confirmed; crash-neutral implementation additionally needs options.
- Standalone yield-change and Nelson-Siegel curvature portfolios: insufficient verified separate trading construction.
- Equity-differential factor, trade-network centrality, sovereign-credit-risk, unemployment, import-ratio, skewness-risk and global-FX-volatility-beta sorts: strategy-specific source details not established within the query budget.
- FX latency arbitrage and standalone dealer inventory market-making: BIS 2011 PDF returned `404 Not Found`; later BIS source retrieval returned `400 Timeout fetching`.
- Retail-flow moving-average contrarian trading from News and intraday retail investor order flow in foreign exchange markets: publisher open failed.
- Liu, Tan and Wang (2020), commodity-average forecasts for AUD/CAD/NZD: publisher open failed; no JSONL row from the snippet.
- Evans-Lyons Understanding Order Flow: NBER open returned `403 Forbidden`; Menkhoff customer-flow strategies were independently sourced instead.
- Directional option strike pinning and barrier-defense rules: not sufficiently sourced. Expiry hedge unwind does not establish those predictions.
- Neural chart-image trading (Sher, arXiv:1111.5892) and ab-initio evolutionary agents (arXiv:1912.09524): abstracts opened, but exact major-pair scope, signal-family mapping and holding construction were not established, so not promoted to keyed strategies.

Additional exclusions by arena, not claims of missing literature: pure volatility/skew swaps, option-only crash overlays, covered-interest/forward-basis arbitrage, emerging-only studies, NOK/SEK-only mandated central-bank programmes, and CME/RavenPack strategies whose only verified implementation was currency-futures-specific. G2-G5/B2-B5 carry parameter subsets were not transcribed individually; the enhanced-carry framework and verified G1/B1 definitions are indexed.

### treasuries — side A (union 476)

These are the gaps a later proposer could exploit to claim a false "novel". Worth a manual re-source before the gate runs.

- **Green (2004), "Economic News and the Impact of Trading on Bond Prices", JF 59(3).** Order flow is substantially more informative in the ~15 minutes after macro announcements. Wiley/Cambridge/SSRN all blocked; DOI confirmed but abstract elided. Strongest single omission.
- **Fleming & Remolona (1997), "What Moves the Bond Market?", FRBNY Economic Policy Review** — the canonical ranking of releases (employment report largest). URL did not resolve.
- **Nakamura & Steinsson (2018), "High-Frequency Identification of Monetary Non-Neutrality: The Information Effect", QJE** — the Fed-information-effect decomposition of policy surprises.
- **Gorodnichenko, Pham & Talavera (2023), "The Voice of Monetary Policy", AER** — vocal-tone hawkishness beyond statement text.
- **Ilmanen (1996), "Does Duration Extension Enhance Long-Term Expected Returns?", Journal of Fixed Income** — duration timing off the term spread / rolldown. Sought by two sub-agents independently; no openable landing page.
- **Fabozzi, Martellini & Priaulet (2005), "Predictability in the Shape of the Term Structure of Interest Rates", JFI 15, 40-53**, and **Martellini & Priaulet (2002), "Understanding the Butterfly Strategy" (EDHEC)** — the canonical bullet-vs-barbell butterfly weighting references. Publisher 404/rate-limit.
- **Duffee (2002), "Term Premia and Interest Rate Forecasts in Affine Models", JF**, and **Fama (1984), "The Information in the Term Structure", JFE 13** — not opened within budget.
- **Cochrane & Piazzesi (2008), "Decomposing the Yield Curve"** — not opened.
- **Amihud & Mendelson (1991)** T-bill/T-note liquidity premium and **Warga (1992)** off-the-run portfolio returns — the on-the-run premium is represented only by Krishnamurthy (2002).
- **Auction "tail" (stop-out yield minus when-issued yield) as a tradable signal**, and **indirect-bidder share as a US demand signal** — only practitioner/blog write-ups surfaced; the euro-area bid-to-cover paper is the recorded academic analogue.
- **Mid-month coupon settlement / coupon-payment reinvestment cycle** as a standalone Treasury flow strategy — nearest sourced proxies are the SOMA rollover FAQ and the Bloomberg index cash-reinvestment row.
- **HBS WP 26-033 "What Treasury Auctions Reveal About Investor Demand"**; **IMF WP 2025/088 on the Treasury buyback programme**; **St. Louis Fed "The Declining Convenience Yield and Quantitative Tightening"** — all returned empty or non-content to fetch.
- **Citi Economic Surprise Index duration-timing overlays** (Macrosynergy, Confluence/ETFTrends) — Cloudflare-blocked. El Ouadghiri et al. covers the surprise-response mechanism but not the index-level overlay.
- **Cheng & Madhavan (2009/2010)**, the original levered-ETF rebalancing paper — only a "Request PDF" landing surfaced; the EFMA 2024 working paper was used instead.
- **Practitioner month-end "index extension" sizing** (InTouch Capital Markets and similar, in years of duration and $bn) — paywalled/LinkedIn.
- **Man Group/AHL, Two Sigma, PIMCO, Bridgewater notes on bond trend/carry/duration timing** — no research-page URL surfaced; the practitioner side of the styles angle rests on AQR, Robeco and Ardea only.
- **Quarter-end/year-end effect in Treasury *futures*** (as distinct from repo) — no direct source.
- **US pension LDI duration demand** as distinct from the UK 2022 episode — no openable source.
- **CTA trend-following in Treasury futures as a named published strategy** — covered obliquely by the COT positioning row and the trend rows, not directly.

Also noted but deliberately *not* keyed as a strategy: **Thornton & Valente (2012), RFS 25(10) 3141**, which finds forward-rate predictability "does not generate any systematic economic value to investors" net of costs. It tests `fama-bliss-forward-spread` and `cochrane-piazzesi-tent-factor` rather than proposing a new signal — but it is the right prior for calibrating any curve-predictability proposal.

### treasuries — side B (union 476)

None of these items was promoted into the JSONL solely from memory, a search snippet, or an unreadable page.

- Arak and Cook (1997): morning reversal after large overnight Treasury-futures moves and daily-limit magnet effects.
- Shynkevich (2016): broad technical-rule search in bond returns, including Treasury ETFs; moving-average, filter, support/resistance and channel families need a readable source establishing their exact Treasury implementation.
- Brooks/Katz/Lustig monetary-policy-surprise drift in US bonds: precise original rule and horizon not recovered.
- Savor/Wilson macro-announcement Treasury premium, and Jones/Lamont/Lumsdaine macro-news bond premium: usable original evidence not recovered here.
- Yield drifts when issuance comes before macro news (JFE 2025): detailed US extension not extracted from a successfully readable article.
- Gao, Hu, Li and Liu (2026): Treasury-futures hedging-pressure and GARCH risk-premium model; publisher and conference PDF opens failed despite useful search snippets.
- Range-based volatility timing using Treasury-bond futures: one Tsinghua PDF open returned a document, but subsequent reads failed and authors/details were not reliably recovered.
- Standalone coupon reinvestment timing, Treasury ETF dividend capture, and option-expiry pinning.
- Quarter-end regulatory balance-sheet contraction as a separately specified return strategy.
- Etula et al., Dash for Cash: a separate detailed Treasury rule was not extracted.
- STRIPS stripping/reconstitution and principal-versus-coupon relative value.
- A specifically defined PCA Treasury butterfly, separate from general curve arbitrage.
- Treasury ETF-futures basis, distinct from ETF-basket creation/redemption.
- Futures convexity-bias calendar trading, distinct from documented delivery options and rolling.
- A distinct profitable strategy against March 2020 margin-called funds: no such claim added. Cai's historical LTCM anticipatory trading is separately sourced.
- Generic news-sentiment strategies demonstrated only in stocks, Chinese/Indian sovereign bonds, or UK gilts were not treated as established US Treasury strategies.

### options — side A (union 477)

- **Max pain / pin-risk targeting** around expiry (practitioner folklore; the academic pinning evidence *is* keyed
  as `sweep-options:expiration-pinning`, the trading rule itself is not sourced).
- **The wheel** (cash-secured put, then covered call after assignment) as a named retail strategy.
- **tastytrade-style mechanical management rules**: 45-DTE entry, 21-DTE roll, 50 %-of-max-profit take, IV-rank /
  IV-percentile entry filters on short strangles.
- **Broken-wing butterfly, ratio spreads, jade lizard** and the rest of the named defined-risk retail structures.
- **CBOE CLL (collar) and WPUT (weekly put-write) benchmark indexes** — the Wilshire benchmark-index PDF was the
  one document I could not open (WebFetch denied), and the search snippets named only BXM, PUT, BXMD, CMBO, CNDR
  with figures. Those five are keyed; CLL and WPUT are not.
- **Pre-FOMC announcement drift (Lucca & Moench 2015)** — referenced inside a search summary, but no page of that
  paper was opened; the event-day/FOMC option rows that *were* sourced are keyed instead.
- **Convertible-bond arbitrage and employee-stock-option hedging as vega supply channels** into listed options.
- **Pension/insurer put-spread-collar overlays** as a standing supply of index skew.
- **Leveraged-ETF end-of-day rebalancing** (the equity leg; the option-hedging channel is keyed via
  `sweep-options:hedging-demand-intraday-momentum`).
- **Single-stock dispersion at desk level via variance swaps** (the index-option form is keyed as
  `sweep-options:correlation-risk-premium-dispersion`).
- **Overnight-versus-intraday decomposition of the index variance risk premium**.

### options — side B (union 477)

These remembered or search-preview ideas did not yield sufficient opened strategy evidence during the budget. They are excluded from the JSONL and are not certified novel:

- Chung and Louis (2017): pre-versus-post earnings straddle rotation; publisher retrieval failed.
- Bali and Murray (2013): delta/vega-neutral skewness assets; direct PDF retrieval failed. This is distinct from the sourced skew-swap rows.
- Han (2008): sentiment-conditioned index-option skew trading; original trading evidence not retrieved.
- Liquidity-risk-beta option portfolios; no original strategy source opened.
- Equity-option implied-volatility-surface forecasting: *Can we forecast the implied volatility surface dynamics of equity options? Predictability and economic value tests*; publisher retrieval failed.
- Jones and Wang term-slope implementation; PDF retrieval failed. Vasquez's independently sourced slope strategy is keyed.
- Gârleanu, Pedersen and Poteshman, *Demand-Based Option Pricing*: demand-conditioned options trading rule not recovered; NBER open returned `Internal Error`.
- Barbon and Buraschi, *Gamma Fragility*: source presentation retrieval failed. Cboe's descriptive hedge mechanics alone were not converted into a newly invented trading rule.
- Ni, Pearson and Poteshman: expiry-date price clustering/pinning strategy; publisher retrieval failed, and the return studied is primarily in the underlying.
- Pool, Stoll and Whaley: nonexercise trading game; publisher retrieval failed. The later Bryzgalova et al. dividend-play implementation is independently sourced and keyed.
- Autocallable structured-product hedging: primary issuance size together with the listed-option hedge rule was not established.
- JPMorgan quarterly collar reset exploitation: source-grounded fund size and a trading rule around the reset were not established.
- Variance-versus-volatility convexity and corridor-variance trades: no adequate strategy source retrieved in this allocation.
- Jelly-roll dividend/financing arbitrage: no primary practitioner/paper body retrieved.
- SPY-SPX ETF order-flow arbitrage from Moussawi, Xu and Zhou, *A Market Maker of Two Markets*: PDF and SSRN body opens failed.
- Short-term intraday morning/afternoon option momentum from *Intraday Option Return: A Tale of Two Momentum*: author PDF body open failed. The separately sourced half-day momentum/reversal study is keyed.

Byun-Kim's MAX10 gambling idea was initially unresolved but was recovered through the opened academic replication and included as `sweep-options:max10`. Gao-Xing-Zhang earnings straddles were recovered through the publisher-supplied RePEc abstract after the author PDF repeatedly timed out; the final row cites that successful body open.

### crypto-micro — side A (union 478)

These are real, known ideas. They are deliberately **not** in the JSONL. A later proposer hitting any of them should still be treated as non-novel; they need a sourcing pass before they can enter the catalogue.

**Blocked by publisher (SSRN, ScienceDirect, Wiley, MDPI, Emerald, OUP, pm-research all 403/Cloudflare):**
- Fan, Jiao, Lu & Tong, "The Risk and Return of Cryptocurrency Carry Trade", SSRN 4666425 — cross-sectional high-minus-low crypto interest-rate carry.
- "The Crypto Carry Trade" (Christin et al., WFA).
- Inan, "Predictability of Funding Rates", SSRN 5576424 — DAR-model out-of-sample funding forecasting.
- Chi et al., 2023, "An empirical investigation on risk factors in cryptocurrency futures", JFM — basis / momentum / basis-momentum factors.
- "Exploring risk and return profiles of funding rate arbitrage on CEX and DEX", 2025.
- "The Two-Tiered Structure of Cryptocurrency Funding Rate Markets", Mathematics 14(2):346.
- Haghani & White, "Perpetual Futures: Mechanics, History and Purpose", SSRN 7059779.
- Alexander & Imeraj, "The Bitcoin VIX and Its Variance Risk Premium", JAI 23(4), 2021.
- Atanasova, Miao, Segarra & Willeboordse, "What Do Crypto Options Tell Us? Risk Premia Implied by BTC Option Prices".
- Grith, Almeida, Miftachov & Wang, "Option-Implied Risk Premia and Cryptocurrency Market Regimes".
- "Implied volatility slopes and jumps in bitcoin options market", Economics Letters.
- Winkel, Härdle, Zhou & Chen, "Option Returns and the risk-free Rate in Crypto Asset Markets".
- "Pricing Kernels and Risk Premia implied in Bitcoin Options", Risks 11(5):85.
- Choi, Lehar & Stauffer, "Bitcoin Microstructure and the Kimchi Premium", SSRN 3189051.
- Muck, Schmidl & Wolf, "Wish or reality? On the exploitability of triangular arbitrage in cryptocurrency markets", FRL 2025.
- Alexander, "Latency Arbitrage in Cryptocurrency Markets", SSRN 5143158.
- Alexander & Heck, "Price discovery in Bitcoin: the impact of unregulated markets", JFS 2020.
- Cong, Karolyi, Tang & Zhao, "Crypto Value, Factor Pricing, and Market Segmentation", SSRN 3985631 — **the crypto value / network-adoption factor paper; the single highest-value gap in this sweep.**
- Zhang & Li, "Is idiosyncratic volatility priced in cryptocurrency markets?", RIBAF 2020.
- Zhang, Li, Xiong & Wang, "Downside risk and the cross-section of cryptocurrency returns", JBF 2021.
- Cakici, Shahzad, Będowska-Sójka & Zaremba, "Machine learning and the cross-section of cryptocurrency returns", IRFA 2024.
- Jia, Liu & Yan, "Higher moments, extreme returns, and cross-section of cryptocurrency returns", FRL 2020.
- Jia, Goodell & Shen, "Momentum or reversal: Which is the appropriate third factor for cryptocurrencies?", FRL 2021.
- "Crypto factor zoo (.Zip)", IRFA 2026 — 36 replicated crypto predictors.
- "Unravelling cross-sectional patterns in cryptocurrencies: a four-factor asset pricing model", CAFR 27(4), 2025.
- Kraaijeveld & De Smedt, "The predictive power of public Twitter sentiment for forecasting cryptocurrency prices", JIFMIM 2020.
- Lucey et al., Cryptocurrency Uncertainty Index (UCRY), FRL 2021.
- Lim, "The Price Impact of Spot Bitcoin ETF Flows", SSRN 6592830.
- "Do FOMC and macroeconomic announcements affect Bitcoin prices?", FRL 2019; "Scheduled FOMC statements and intraday macro event risk in cryptocurrency markets", FRL 2026; "Monetary policy shocks and Bitcoin prices", RIBAF 2022.
- Long, Jiang & Zhu, "Seasonality in the Cross-Section of Cryptocurrency Returns", FRL 2020 (the *Finance Research Letters* variant; the 2020 same-weekday paper IS catalogued).
- "Calendar effects on returns, volatility and higher moments: Evidence from crypto markets", NAJEF 2025.
- "Is there an expiration effect in the bitcoin market?", IREF 2023.
- "One year of bitcoin spot ETPs", Economics Letters 2025.
- "Valuing cryptocurrencies: A model of price and hashrate", FRL 2025.
- Shen, Urquhart & Wang, "A three-factor pricing model for cryptocurrencies", FRL 2020; Liu, Liang & Cui, "Common risk factors in the returns on cryptocurrencies", Economic Modelling 2020; Bianchi & Babiak, "A factor model for cryptocurrency returns".

**Blocked by rate-limit or rendering:**
- Grayscale Research, "The Trend is Your Friend: Managing Bitcoin's Volatility with Momentum Signals" (HTTP 429).
- T3 Index BVIV / BitVol crypto-VIX methodology.
- Ribbon Finance / DeFi Option Vault (Theta Vault) covered-call and cash-secured-put yield programmes.
- Israelov et al., "The Risk-Reversal Premium" (cited as the academic foundation of the Amberdata risk-reversal work, but not opened).
- CME Group, "Bitcoin Options: Volatility Spikes and Recovery Signals" (cmegroup.com 403 throughout, including contract specs).

**No source located at all — remembered or practitioner-folklore only:**
- NVT ratio and Network-Value-to-Metcalfe (NVM) as tested return predictors — practitioner blogs only; the catalogued `btc-metcalfe-lppls-bubble` row is the nearest academic analogue.
- Miner position index, Puell multiple, miner selling pressure, hashrate/mining-cost floor as return signals.
- Whale-wallet, dormancy, coin-days-destroyed and SOPR as standalone signals (MVRV/NUPL/CVDD *are* catalogued).
- Crypto-equity lead-lag (COIN / MSTR versus BTC).
- Open interest and long/short account ratio as a standalone positioning predictor — market commentary only.
- Maker-taker fee and rebate capture in crypto.
- Liquidation-hunting / stop-cluster targeting framed as a strategy (the catalogued liquidation papers are risk/early-warning framed).
- Intraday BTC→altcoin lead-lag at HFT horizon on perps (only daily-frequency spillover papers surfaced).
- CME weekend gap fill; turn-of-the-month in crypto; crypto index (Bitwise/CoinDesk) reconstitution effects; token-unlock/vesting-cliff event studies; the 4pm-NAV-window ETF creation/redemption trade.
- Perp-versus-quarterly calendar spread as a studied strategy; stablecoin lending rate versus funding spread; a dedicated term-structure slope factor for crypto futures.
- Betting-against-beta and long-run (12m+) reversal in crypto — no dedicated paper exists; only the catalogued LTW nulls speak to either.
- Textbooks — none surfaced in any angle.
- AQR, Man Group, Alpha Architect and bank research on crypto — none opened. Practitioner research in the catalogue comes from BIS, NY Fed, CF Benchmarks, Deribit Insights/Amberdata, Flow Traders and Concretum instead.

### crypto-micro — side B (union 478)

The following were not admitted as separate JSONL strategies; some have a source in another market or an inaccessible candidate citation.

- Perp-specific news/social-sentiment and COT-following strategies: opened Beyond pure hype (Review of Derivatives Research, 2026) uses CME dated futures, not perps; excluded.
- BTC option expiry intraday reversal paper (ScienceDirect S1544612326008688): open returned Internal Error. Other independently sourced expiry/gamma strategies retained.
- Quanto/inverse cross-contract convexity arbitrage: BitMEX article redirected to the blog landing page; no usable strategy body.
- Crypto index-versus-components implied-correlation dispersion: searches returned equity-option sources, no crypto-specific implementation.
- AMINA CoinDesk Bitcoin Momentum Strategy: opened bank factsheet describes a tracker certificate and BTC allocation, not a documented BTC perp/options implementation; excluded.
- Felman (2021) Momentum, Bitcoin and Reflexivity: search located BTC spot trend tests; no explicit perp implementation opened; excluded.
- Extreme negative funding predicting subsequent BTC spot returns (Memon et al., 2026): opened source, but return target is spot; not separately keyed as a perp backtest.
- IBIT option/CME carry wedge: identifiable source, but ETF options and dated futures lie outside this arena's two object tokens.
- Futures grid trading: no adequate opened BTC/ETH practice source in the allocated searches.
- RSITrend200EMA, TEMA/ATR and AdaptiveVolatilityStrategy: MDPI page https://www.mdpi.com/2227-7390/14/5/761 failed to open.
- Adaptive funding-aware reinforcement-learning market making: https://www.sciencedirect.com/science/article/pii/S240591882600022X could not be fetched; its journal issue is December 2026. Separate sourced HJB and classical market-making entries are retained.
- CEX/DEX funding arbitrage paper: https://doi.org/10.1016/j.bcra.2025.100354 failed to open. Independently sourced cross-venue funding practice is retained.
- De Blasis/Webb contract-design and seasonal effects: https://onlinelibrary.wiley.com/doi/full/10.1002/fut.22305 failed to open.
- Adaptive copula and Alpha Overlay: opened institutional record did not establish BTC/ETH membership in the studied perpetual contracts; not keyed.
- Copula-based trading of cointegrated cryptocurrency pairs: source at https://link.springer.com/article/10.1186/s40854-024-00702-7 did not clearly establish the narrow BTC/ETH-perp object.
- Alexander et al., Arbitrage Opportunities and Efficiency Tests in Crypto Derivatives: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4495548 returned Internal Error. Separate documented parity practice retained.
- Put-call parity in a crypto option market - Evidence from Binance: https://www.sciencedirect.com/science/article/abs/pii/S1544612323012461 returned Internal Error.
- Explicit Bitcoin option box-spread arbitrage: no adequate successfully opened primary strategy source.
- Daily 0DTE ATM straddle selling: The BTC Volatility Surface: Q1, 2023 was readable to the actor researcher but intermittent Internal Error responses prevented consistent synthesis retrieval; left out conservatively.
- Separate ETH Merge event-volatility rule: event discussion found, independently specified strategy not established.
- Trading ahead of Ethena mint/redemption hedges: mandated flow is documented, profitable anticipation by outsiders is not. The actual institutional hedge practice is catalogued.
- IBIT cash-flow/expense-sale anticipation specifically through perpetuals: not established; actor rows correctly say none known.
- Predictable crypto benchmark month-end tracker rebalancing: insufficient sourced mandate and size.
- Tax-calendar BTC/ETH perpetual selling: no usable opened strategy citation.
- ADL-triggered automatic hedge restoration by basis funds: mechanics established, documented restoration strategy not established.
- Exact max-pain forecasting strategy: definitions surfaced, no sourced forecasting implementation.
- Funding-window sniping: no implementable rule established; Deribit funding accrues continuously.
- Protective-collar and standalone naked-call/put timing rules: generic option payoffs are familiar, but no distinct sourced timing rule retained.

### bond-etf-nav — side A (union 479)

Real, known ideas in this arena that no page opened this session supports. They are **not** in the JSONL. A later novelty gate should treat every one of them as KNOWN anyway and a proposer re-inventing one should not clear the gate.

**Blocked by Cloudflare / paywall (SSRN, ScienceDirect, Wiley, Oxford Academic):**
- Dannhauser (2017, JFE) "The impact of innovation: Evidence from corporate bond ETFs" — bond-level ETF ownership lowering yields. Named in three opened sources' citation lists; its own page never opened. The most important gap in this sweep.
- Dannhauser & Karmaziene, "The Dealer Warehouse — Corporate Bond ETFs" (SSRN 4613818) — bonds with more bid-side volume enter creation baskets; ahead of downgrades/earnings misses ETF holdings absorb a large share of institutional net selling.
- Goldstein, Jiang & Ng (2017, JFE) "Investor flows and fragility in corporate bond funds" — concave flow-to-performance, first-mover advantage.
- Choi, Hoseinzade, Shin & Tehranian (2020, JFE) "Corporate bond mutual funds and asset fire sales".
- Jiang, Li, Sun & Wang (2024, RFS) "Bond Price Fragility and the Structure of the Mutual Fund Industry".
- Avramov, Chordia, Jostova & Philipov, "The Distress Anomaly is Deeper than you Think: Evidence from Stocks and Bonds" (SSRN 3702508) — the distress/quality entry for credit.
- Bai, Bali & Wen, "Is There a Risk-Return Tradeoff in the Corporate Bond Market?" (SSRN 3401231).
- Baltussen, Muskens & Verwijmeren, "The Cross-Section of Corporate Bond Returns" (SSRN 5130312).
- Kelly et al. (2023, Journal of Finance) "Modeling Corporate Bond Returns".
- Dick-Nielsen, "Corporate Bond Factors: Replication Failures and a New Framework" (FoFI 2024).
- AP regulatory constraints and limits to ETF arbitrage in the March 2020 dash-for-cash (JBF 2025, S0378426625001190).
- "Fast ETFs, slow bonds: price adjustment under monetary tightening" (Finance Research Letters, S1544612325026340).
- Agapova, Volkov et al., Financial Review 2025 journal version of the ETF-ownership/bond-volatility result (the 2018 AEA conference version *was* opened and is keyed).
- Cointegration-based ETF pairs trading with named HYG/JNK and LQD/VCIT pairs (Journal of Asset Management 2025, 10.1057/s41260-025-00416-0) — I fetched it; Cloudflare interstitial.

**Cited only inside sources that were opened, never opened themselves:**
- Chalmers, Edelen & Kadlec (2001) — the mutual fund "wild card" option (seen inside Qian 2008).
- Engle & Sarkar (2006) — duration and persistence of ETF premiums and discounts.
- Madhavan & Sobczyk (2014) — persistent and systematic ETF mispricing.
- Coval & Stafford (2007) — asset fire sales / flow-driven price pressure.
- Broman (2016) — ETF premium/discount comovement and the size gradient (its numbers reach the catalogue only via NBER w22829, which *was* opened).
- Fed / NY Fed SMCCF primary documents (the SMCCF rows are sourced to Citi, NBER, Chicago Fed and FRBNY EPR instead).

**No source surfaced within budget (genuine coverage gaps for this arena):**
- SPY→HYG intraday lead-lag / equity price discovery into high-yield ETFs.
- HYG-vs-CDX-HY basis as a tradable signal (the CDS/CDX basis rows in the catalogue are cash-bond and index-CDS, not ETF-vs-CDX).
- Bond-ETF options specifically: HYG/LQD/TLT variance risk premium, put-call parity violations, short squeezes, securities-lending fee dynamics. The one options row in the catalogue is a stock/levered-ETF gamma study.
- An explicit TLT↔HYG risk-on/risk-off rotation rule.
- VIX or a credit VIX (VIXHY) as a standalone credit-timing signal (S&P education material and Soper & McAlley are Cloudflare/Akamai-blocked).
- TIPS breakeven momentum/carry rules (only the TIPS-Treasury basis is sourced).
- CPI/NFP surprise effects measured on bond *ETFs* rather than on Treasury futures or cash.
- Month-end index-extension *sizing* for the 1yr+ UST index (~0.11 years extension, ~$319bn supply) — snippet only.
- January HY spread seasonality magnitudes (~16 bp) — the opened Sage Advisory text carried only the IG 4 bp figure, which is what the catalogue records.
- Bond-ETF close (mid) vs NAV (bid) valuation-convention wedge, and bond-ETF tracking difference / cash drag — the VanEck whitepaper downloaded but its text was never extracted (`pdftotext` denied) and the NYU Stern Kolotiy paper was never opened.
- Bond-ETF cross-sectional/asset-class ETF momentum rotation and vol-targeting/risk-parity across bond ETFs — angle 6's candidate pages (SMU working paper, CXO SACEMS, MDPI duration rotation) were never opened; the two rows the catalogue does carry for this territory (`volatility-managed-portfolio`, `etf-arbitrage-noise-channel`) are keyed to their real equity objects, not to bond ETFs.

### bond-etf-nav — side B (union 479)

1. Jiang, Li, Tang and Xiao (2025), *Machine Learning Equity Signals for Corporate Bond ETFs*: constituent-stock lead-lag; nonlinear economically structured GBT; combined signals; randomized-stock and unregularized-GBT placebos. Search exposed the abstract and the author homepage opened, but paper retrieval failed (403/Internal Error). Paper URLs: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4049277 and https://papers.ssrn.com/sol3/Delivery.cfm/SSRN_ID4495838_code1638475.pdf?abstractid=4049277&mirid=1&type=2 . Author listing alone was not treated as evidence for the detailed rules.
2. *Fast ETFs, slow bonds: price adjustment under monetary tightening*, Finance Research Letters: next-day ETF–NAV convergence after rate changes. Publisher open failed: https://www.sciencedirect.com/science/article/pii/S1544612325026340 .
3. *Authorized participants' regulatory constraints and limits to ETF arbitrage during market turmoil*, Journal of Banking & Finance: publisher open failed: https://www.sciencedirect.com/science/article/pii/S0378426625001190 .
4. Goldberg and Ronn (2025), FLOT/LQDH arbitrage. University bibliographic record opened but contained no method; SSRN paper and DOI retrieval failed. No execution rule was inferred from the title. https://scholarlyworks.adelphi.edu/esploro/outputs/journalArticle/Testing-an-Arbitrage-Strategy-between-FLOT/991004487763406266 .
5. *Using ETF Premia to Measure Corporate Bond Liquidity* (Flannery, Nimalendran, Ray and Yousefi): original paper not fetched.
6. Yun (2026), LQD stress predicting HYG stress, SSRN 6765039: PDF returned 403.
7. Corporate-bond January tax-loss seasonality, *Return seasonality and tax-loss selling in the market for long-term government and corporate bonds* (JFE, 1986): publisher retrieval failed; no recalled authors/statistics keyed.
8. Dick-Nielsen, *Three Essays on Corporate Bond Market Liquidity*, index inclusion/deletion pressure: PDF retrieval failed.
9. Antonacci absolute momentum specifically applied to corporate/EM bond ETFs: no sufficiently specific original implementation sourced.
10. Generic corporate/EM ETF factor size, quality, carry and cross-sectional momentum beyond the explicit retained ETF methodologies: underlying credit evidence does not alone establish the ETF implementation.
11. Automatic ETF distribution reinvestment as a forced actor: no directly applicable reinvestment-flow size sourced.

The HYG/JNK sourcing gap initially reported by the arbitrage sub-agent was resolved by Chen/Alexiou; it is included in the pairs rows.

### microcap — side A (union 480)

These are real, well-documented microcap-arena ideas I could not put a session-opened URL behind inside the search budget. A later proposer claiming any of them is **not** novel; they should be swept in a follow-up sitting.

- Idiosyncratic / residual momentum in small caps (Blitz, Huij, Martens 2011) and momentum crashes in the small-cap tail (Daniel & Moskowitz 2016)
- Net operating assets (Hirshleifer, Hou, Teoh, Zhang 2004) — a balance-sheet-bloat screen strongest in small stocks
- Beneish M-score earnings-manipulation screen applied to microcaps
- Spin-off and corporate-restructuring drift (Cusatis, Miles, Woolridge 1993), including microcap spin-off parents
- Firm age / years-since-listing as a cross-sectional predictor
- Roll (1984) high-low and Corwin–Schultz spread estimators, and Lesmond–Ogden–Trzcinka zero-return days — standard microcap cost lines
- Day-of-week / Monday and turn-of-the-month effects in small caps (Keim & Stambaugh 1984)
- Closed-end fund discount as a small-firm sentiment proxy (Lee, Shleifer, Thaler 1991)
- SEC tick-size pilot (2016–2018) effects on small-cap liquidity and quoted spreads
- Microcap merger arbitrage and going-private / minority squeeze-out spreads
- SPAC and shell-trust arbitrage in the microcap listing tier
- Retail short-squeeze / meme dynamics in low-float microcaps (2021 onward literature)
- Dimensional's small-cap implementation rules (exclusion of small-growth and high-asset-growth junk, patient trading)
- Index-fund front-running of the Russell reconstitution specifically documented by Madhavan (2003) and Chen, Noronha, Singal (2004)

### microcap — side B (union 480)

These ideas were remembered or surfaced as leads but lacked adequate qualifying evidence for another JSONL entry:

1. Conventional short-term small-stock reversal and high-volatility conditioning (Stivers-Sun / SSRN 1911506): search lead, SSRN fetch failed.
2. Long-run loser reversal (De Bondt-Thaler): no confirmed source-restricted small-only implementation.
3. Ritter (1988) individual-investor turn-of-year reinvestment: publisher open failed. Reinganum's separate January patterns are included with the narrower search-abstract qualification above.
4. Keim-Stambaugh (1984) small-stock Friday/weekend pattern: author PDF supplied no parsed text and usable screenshots were unavailable.
5. Microcap short-interest levels/changes and borrow-cost screens: publisher search leads; successful content fetch and exact small-only constructions not established.
6. MAX lottery preference: original paper opened, but a restricted small-only portfolio was not established; small-heavy broad portfolios alone were insufficient.
7. Coval-Stafford fund-fire-sale reversal: general-equity evidence located, small-only implementation unverified.
8. Standalone R&D/market, advertising, organization capital and intangible-adjusted value: no verified small-only construction in opened sources.
9. Odd-lot tender priority and reverse-split cash-outs: general practice sourced, but reviewed detailed examples did not establish the required small-cap restriction. AHOM's distinct take-private trade is included.
10. Smallcap liquidation discounts and demutualizations: practitioner leads found; exact US small-only scope was not sufficiently established for additional rows.
11. Microcap delisting, margin-call and borrow-recall exploitation: no qualifying sourced implementation within budget.
12. Russell quarterly IPO inclusion and smallcap leveraged-ETF-flow exploitation: mechanics located, specific exploitation strategy not sourced.
13. Pure small-minus-big and cold-minus-hot turnover size factors: overall constructions have a large-stock leg; not admitted as US small-only cross-sections.
14. AQR standalone small profitability/growth/safety/payout components: identified within the opened QMJ construction, but not separately keyed because independent component strategy detail/statistic extraction was incomplete. QMJ's composite records those known inputs.
15. Other ratios/filters or signal interactions not directly extracted from the bounded source set remain unenumerated. This list is not a novelty endorsement.
