# F1 etf-primary-flow-reversal-month — the issuers' terms, read before any fund-data parse (2026-11-18, ledger lines 29–32)

Each host's robots, then its terms, each one request through `rawFetch` into its depot. Each terms page was quoted
before any fund export was parsed. The terms URLs were found by web search, so no other page on these hosts was asked.

- **Invesco** (line 29, depot `invesco`). Robots #1: `User-agent: *` opens the site except the query parameters listed
  (`/*asOfDate=`, `/*startDate=`, `/*endDate=`, … `/*.zip`). Terms #2 (`www.invesco.com/us/en/resources/terms-of-use.html`,
  "These Terms were last updated on May 6, 2018"):
  - the licence is "to access and make personal use of the Website, but not to download (other than page caching …) or
    modify them, or any portion of them, except with the express prior written consent of Invesco";
  - the prohibited uses are "Use devices (including software) that are designed to provide repeated automated access to the
    Website other than those made generally available by Invesco" and "use any data mining, robots, or similar data
    gathering and extraction tools on the Website".

  No storage or AI clause, so the amendment's (4) does not strike line 29. But the terms bar the automated read itself,
  as Nvidia's § 3.2 (f) does (D818, `govern/receipts/d818-nvidia-terms.md`). So no Invesco page past #2 was asked.
  **Line 29 reads nothing more under these terms:** QQQ, DBA, DBC, UUP, FXE and FXY are not read.
- **SPDR** (line 30, depot `ssga`). Robots #293: `User-agent: *`. Its `Disallow` lines name `/library-content/assets/pdf/documents`
  and other paths, but not `/library-content/products/fund-data/`. Terms #294
  (`www.ssga.com/us/en/institutional/ic/footer/terms-and-conditions`, no dated line):
  - "You may not copy, reproduce, duplicate, modify, adopt or lend, sell, disseminate or otherwise transfer … any of the
    information contained in this Site, except for the purpose of accessing the Site and producing print-outs for your own
    personal use, or making a reasonable number of copies of such pages for internal use";
  - (iv) bars information "to be published, redistributed or retransmitted".

  There is no automated-access, storage or AI clause. The ETF site's legal page (#295) renders no text without script.
  **Line 30 stands, under its redistribution limit:** values stay in the depot and git-ignored data, and receipts quote
  aggregates alone. SPY's navhist export is #296 (200, xlsx, one request). GLD's is the gold fetcher's held #290 of
  2026-11-18, not asked again.
- **USCF** (line 31, depot `uscf`). `robots.txt` (#1) answers 200 `text/html` with the site's HTML sitemap, so there is no robots file.
  Terms #2 (`www.uscfinvestments.com/terms-of-use`):
  - "You agree not to (i) use or launch any automated system, including without limitation, "robots," "spiders,"
    "offline readers," and any other similar or analogous system";
  - the Content "may not otherwise be reproduced, distributed or transmitted to any other person or incorporated in any
    way into another database".

  The database clause forbids storage, which **strikes line 31 under the amendment's (4)**. USO is not read.
- **Vanguard** (line 32, depot `vanguard`). Robots #1: `User-agent: *`, `Disallow: /images/`, `/static/`, `/404`. Terms
  #2 (`investor.vanguard.com/terms-conditions`):
  - the licence lets you "view, store, bookmark, download, and print the pages within this Site solely for your personal,
    informational, and noncommercial use";
  - barred conduct includes "using devices or software that provide repeated automated access to this Site, other than
    those made generally available by Vanguard".

  Storage is licensed, so line 32 is not struck, but the automated read is barred, as with Invesco. **Line 32 reads nothing
  more under these terms:** VNQ is not read.
- **iShares** (the 2026-11-14 (K1) line's (1), its terms depot `blackrock` #3, extended by D881 (a)). The seven roster
  exports not already held were each asked once, by D851's link pattern off LQD's held page (`ishares` #4):
  - IWM #29, EFA #30, EEM #31, TLT #32, IEF #33, TIP #34 and SLV #35, all 200 SpreadsheetML;
  - LQD #4, HYG #8 and EMB #12 were already held from D851.

  Each `Historical` sheet carries a daily `Shares Outstanding` from the fund's inception, restated to today's share basis.

Effect: the row ranks 12 of the roster's 20 funds: iShares 10 plus SPY and GLD. They cover equity, fixed income and
commodities, so the two-class rule can still bind. D881 (a) has a fund with no daily history fall out of the eligible set,
and a fund whose terms bar its read falls out the same way. This was taken under the 10-31 filter and is reversible by an
inbox block, before the probe. The probe is never re-run, so a waiver after it reaches only
`etf-acquisition-cost-overhang-year`, the other row on these lines.
