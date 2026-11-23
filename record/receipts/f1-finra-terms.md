# F1 `probe:etf-executed-short-flow-month` — FINRA's terms, read for ledger line 27 (2026-11-17): struck

This was a headless sitting (`/resume P1 headless`). It cost $0 and read bytes only: robots, the terms and the data's catalogue page. No
short-sale file, symbol, volume or price was asked for or read.

- **Admission:** `govern/source-admissions.jsonl` line 27, depot `finra` (D879, `f7b09b31`, Amendment 2026-11-11 (K1),
  `c552396a`). The line's licence clause says: "terms that forbid storage or AI use strike the source (the amendment's (4))".
- **Order:** robots came first on both hosts. The terms went into the depot and are quoted here before any parse. Each request was one
  `rawFetch` (`.review-scratch/f1-short-flow/pull.mjs`, ignored scratch), into depot `finra` #68–#72, 2026-11-17
  18:49–18:50 ET.

## Robots

| host | robots.txt (row) | reading |
|---|---|---|
| cdn.finra.org | #68 | HTTP 403, `<Code>AccessDenied</Code>` (111 bytes, an object store with no robots object). No rule, so the host is open. |
| www.finra.org | #69 | HTTP 200, 156 rule lines in one `User-agent: *` group with no crawl delay. It closes Drupal paths (`/core/`, `/admin/`, `/search/`, `/user/…`) and five PDF reports on generative AI. `/terms-of-use` and `/finra-data/` are open. |

## Terms

`/terms-use` (#70) is a 404, and its footer links `/terms-of-use`. The terms page is **#71**,
`https://www.finra.org/terms-of-use`, sha256 `d8137e5f…`, 90,575 bytes, "Last modified: November 9, 2023". Its scope is
"The use of the FINRA.ORG site, including all of its content (“FINRA Website”)".

The data's own page (#72, `/finra-data/browse-catalog/short-sale-volume-data/daily-short-sale-volume-files`, sha256
`89fcf95e…`) links no terms but `/terms-of-use`. No data-specific licence displaces the site's.

- **Permitted uses:** "the content and material provided through the FINRA Website shall be used ONLY for your own
  non-commercial personal or professional use."
- **Copyright (b):** the works of authorship "may not be copied, reproduced, transmitted, … altered, **stored for
  subsequent use**, or otherwise used in whole or in part in any manner without FINRA's prior written consent, except to
  the extent that such use constitutes "fair use" …".
- **Restrictions:** "In no case may you:" includes
  - "(d) develop or create a database of data using the FINRA Website, except as expressly permitted by any other terms
    of use on the FINRA Website;"
  - "(e) use any process to monitor or copy the FINRA Website in bulk, or use any data mining, scraping or harvesting
    tools (including robots), or any similar data-gathering or extraction tools;"
  - "(m) use any portion of the FINRA Website in the development of any software program or in conjunction with any
    machine learning, neural network, deep learning, **predictive analytics or other artificial intelligence** computer
    or software program, including, without limitation, by using any portion of the FINRA Website in conjunction with a
    model, algorithm, or process that is designed to predict trades for or within an individual portfolio, fund, or
    other investment vehicle;"
  - "(o) use the FINRA Website for any purposes for which you have not been granted written permission by FINRA."

## Coverage (the catalogue page, #72)

"The earliest date for the Consolidated NMS files is August 1, 2018. The earliest date for the FINRA/Nasdaq TRF Chicago
files is September 10, 2018." The per-facility files (the FINRA/Nasdaq and FINRA/NYSE TRFs, the ADF and the ORF) are
listed back to 2009. Line 27 admits `CNMSshvol<YYYYMMDD>.txt` alone, and that file starts inside the ETF arena's
confirmation window (2016-01-04 →; before it, Sharadar `funds` to 2015-12-31, K1 line 2026-11-02). No file the line
admits therefore lies in the discovery window that a probe may read.

## Judgement

- **Struck.** (b) bars storage "for subsequent use". (m) bars use with "predictive analytics or other artificial
  intelligence", which names a model that predicts trades for a portfolio. Each one strikes the source on its own (the
  amendment's (4)), as AWS's download limit and Microsoft's copy limit did in `govern/receipts/d855-status-archive.md`.
  (e) on its own, a ban on automated gathering, would strike nothing (the 10-10 ruling).
- **Nothing was parsed past the terms, and no data file was asked for.** Rows #68–#72 stay (the depot is append-only). The
  struck line reads no further.
- **An inbox block offers the source to the operator** (D882, the amendment's (4)). Its title carries
  `[factory:probe:etf-executed-short-flow-month]`, so `factory-state` skips the row until the operator answers.
- **Not reached here:** depot `finra` rows 1–67 are `api.finra.org`'s `treasuryDailyAggregates`
  (`server/services/fetchers/finraTrace.js`). They are read under their own line and the operator's 2026-09-11 OAuth ruling, and
  this receipt does not judge them.
