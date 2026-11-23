# F1 `probe:etf-currency-fundamental-value-quarter` — the terms of ledger lines 21–23 (2026-11-17): two of the three pages refused the read

This was a headless sitting (`/resume P1 headless`). It cost $0 and read only robots and terms pages. No series, release, exchange rate or price was asked
for or read.

- **Admissions:** `govern/source-admissions.jsonl` lines 21 (`oecd`), 22 (`brookings`) and 23 (`imf`) (D879,
  `f7b09b31`, Amendment 2026-11-11 (K1), `c552396a`). The row's FX leg is held (`govern/receipts/fx-tape-2026-09-15.json`).
- **Order:** robots came first on each host, then each terms page went into the depot before any parse. Each request was one `rawFetch`
  (`.review-scratch/f1-short-flow/pull.mjs`, ignored scratch), 2026-11-17 19:00 ET.

## Robots

| host | row | reading |
|---|---|---|
| sdmx.oecd.org | `oecd` #1 | HTTP 404, no robots file, so the host is open. |
| data-explorer.oecd.org | `oecd` #2 | `User-agent: *`, `Allow: /`. It closes the archive tenant's query parameters alone. |
| www.oecd.org | `oecd` #3 | `User-agent: *` closes `/content/dam/oecd/` and `/adobe/dynamicmedia/deliver/`. `/en/about/` is open. |
| www.brookings.edu | `brookings` #1 | Its `*` groups close search queries and named uploads (CVs, transcripts, survey tables). The EWN page and its files are not named. |
| data.imf.org | `imf` #1 | HTTP 404 (the portal's own 404 page), no robots file, so the host is open. |
| www.imf.org | `imf` #2 | `User-agent: *` closes twelve `/external/…` and `/forum/`, `/presentation/` paths. `/en/About/` and `/external/terms.htm` are open. |

## Terms

- **OECD** (`oecd` #4, `https://www.oecd.org/en/about/terms-conditions.html`): HTTP 403, "Just a moment... Enable
  JavaScript and cookies to continue", Cloudflare's challenge. Under the 10-10 gathering ruling's limits this **ends
  the read**, with no retry. The same rule dropped OpenAI (D855) and Deribit's terms (D870). The SDMX and Data
  Explorer hosts link no other copy (`oecd` #1 has no link).
- **IMF** (`imf` #3, `https://www.imf.org/en/About/copyright-and-terms`): HTTP 403, "Access Denied … You don't have
  permission to access … on this server", an Akamai refusal. **The read ends**, with no retry. The data portal's footer
  "Copyright and Usage" names `https://www.imf.org/external/terms.htm` (in `imf` #1). That is the same host, which has
  refused this session, so it was not asked.
- **Brookings** (`brookings` #2, `https://www.brookings.edu/terms-of-use/`, HTTP 200, sha256 `3843626e…`):
  - "Brookings grants you … a limited, revocable, nonexclusive, nontransferable, and non-sublicensable license to
    access and make personal use of this site. This license does not include any resale or commercial use of this site
    or its contents; … any derivative use of this site or its contents; … or any use of data mining, robots, or similar
    data gathering and extraction tools."
  - "Upon termination, you must destroy all copies of any aspect of the site in your possession."
  - No passage bars storage or AI use. A ban on automated gathering alone strikes nothing (the 10-10 ruling). **Not
    struck**: taken under the 10-31 filter, and reversible by an operator ruling (the amendment's (3)).

## Judgement

- **The probe cannot read its X.** Line 21's OECD leg holds the CPI, productivity and output-gap inputs, and line 23's
  IMF leg holds export quality. Neither terms page could be read before a parse, as the amendment's (4) requires. No
  data request was made on any of the three lines.
- **An inbox block offers the row to the operator** (D884). Its title carries
  `[factory:probe:etf-currency-fundamental-value-quarter]`, so `factory-state` skips the row until the operator answers.
- **Rows** `oecd` #1–#4, `brookings` #1–#2 and `imf` #1–#3 stay (the depot is append-only).
