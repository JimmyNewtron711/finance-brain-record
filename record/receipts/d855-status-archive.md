# D855 — the chokepoints program's forward archive: status pages and the FAA's NAS status (2026-11-15)

Headless sitting `7772d95f-963a-4111-8b4d-549af70ddd03` (`/resume P1 headless`). $0, bytes only, no return read.
Admission: `govern/source-admissions.jsonl` lines 5–14 (`ee718b12`) and 15 (`93c8f227`), each committed and mirror-pushed
before its probe ran (Amendment 2026-11-11 (K1), `c552396a`). Probe: `scripts/probe-chokepoints-c5.mjs` section 426
(depot `status_pages` #1–#40) and its follow-up 427 (#41–#60), each run once. Robots first, every host; the terms read
into the depot and quoted here before the fetcher parses anything.

## Robots

| host | robots.txt (row) | reading |
|---|---|---|
| www.githubstatus.com, status.claude.com, status.alpaca.markets, status.databento.com | #1, #10, #19, #23 (and #46–#52) | `User-agent: *` / `Disallow: /api/` / `Disallow: /embed/` — Statuspage's own file: **the API is closed to every agent**, so not asked; the history feed each page advertises (`<link rel="alternate" … /history.atom>`) is open |
| status.anthropic.com | #9 | 301 to status.claude.com, read there |
| www.cloudflarestatus.com | #5, #54 | `User-agent: *` / `Allow: /` |
| status.cloud.google.com | #26, #57 | `User-agent: *` / `Disallow:` (open) |
| status.openai.com | #15 | 404 (open) |
| azure.status.microsoft | #29, #59 | 404 (open) |
| health.aws.amazon.com | #33 | 404 (open) |
| nasstatus.faa.gov | #38 | `User-agent: *`, no rule (open) |
| docs.github.com, www.cloudflare.com, www.anthropic.com, openai.com, policies.google.com, www.microsoft.com, aws.amazon.com, www.atlassian.com | #3, #7, #13, #17, #21, #31, #35, #41 | open for the terms pages read (www.cloudflare.com's names `Anthropic-AI` and `Claude-Web` `Allow: /`) |

## Terms, quoted, and the reading of each (the amendment's (4): terms that forbid storage or AI use strike the source)

The screen in sections 426/427 prints each passage naming storage or AI use and strikes on one that also forbids. It
fired on GitHub, Cloudflare, Google and Microsoft, and missed AWS's licence clause (worded as a grant's limit, not a
"may not"); every terms page was then read for limits on downloading, copying or storing. A ban on automated gathering
alone strikes nothing (the operator's 10-10 gathering ruling).

- **Atlassian** (product terms #43, via #42's 301; customer agreement #45, via #44's 301): the Terms of Service that the
  GitHub, Claude, Alpaca and Databento status pages name. 66 and 88 passages name terms; 43 and 41 name storage or AI
  use; none forbids either, and neither page limits downloading or copying. **Not struck.**
- **GitHub** (#4, its terms of service): "You may not duplicate, copy, or reuse any portion of the HTML/CSS, JavaScript,
  or visual design elements or concepts without express written permission from GitHub." / "You may not use the API to
  download data or Content from GitHub for spamming purposes…" The site's design and spam, not status data or AI use.
  **Not struck.**
- **Anthropic** (#14, its consumer terms): "To develop any products or services that compete with our Services,
  including to develop or train any artificial intelligence or machine learning algorithms or models or resell the
  Services." / "To crawl, scrape, or otherwise harvest data or information from our Services other than as permitted
  under these Terms." A ban on training a competing model and on gathering (the 10-10 ruling); no storage limit.
  **Not struck.**
- **Cloudflare** (#8, its website terms): "ARTIFICIAL INTELLIGENCE RESTRICTION You may not use automated bots to access,
  scan, scrape, data mine, copy, or use the materials or content on this website for developing, training, fine-tuning,
  or otherwise contributing to or improving a machine learning model or artificial intelligence (AI) system or the
  operation thereof, unless your bot's user agent is (i) explicitly permitted ("allowed") to do so in this website's
  robots.txt…" The clause's own exception is met: www.cloudflare.com's robots allows every agent and names Anthropic's
  `Anthropic-AI` and `Claude-Web` `Allow: /` (#7), and the status host's allows every agent (#5). The status page itself
  links no terms. **Not struck**: taken under the 10-31 filter; reversible by an operator ruling (the amendment's (3)).
- **Google** (#28, its terms, for Google Cloud's status): "You may not copy, modify, distribute, sell, or lease any part
  of our services or software." / "…our Generative AI Prohibited Use Policy…" / "You may not use this content without
  that person or organization's permission…" (other people's content inside Google's services). The services and
  software, not the incident data; the AI policy binds Google's generative services. **Not struck.**
- **AWS** (#36, the AWS Site Terms): "AWS grants you a limited license to access and make personal use of the AWS Site
  and not to download (other than page caching) or modify it, or any portion of it, except with express written consent
  of AWS." **Struck**: the licence excludes downloading beyond page caching, a storage limit. The probe's one read stands
  (#37; the rows stay). An inbox block offers the source to the operator.
- **Microsoft** (#32, its terms of use, for Azure's status): "You may not modify, copy, distribute, transmit, display,
  perform, reproduce, publish, license, create derivative works from, transfer, or sell any information, software,
  products or services obtained from the Services." **Struck**: copying information obtained from the services, a storage
  limit. The probe's one read stands (#60). The same inbox block.
- **OpenAI** (#18): HTTP 403, "Enable JavaScript and cookies to continue", a challenge. **Dropped**: no terms read, so its
  status page is never parsed or polled; never asked again (the 10-10 limit).
- **Alpaca and Databento**: their status pages' first terms link was the reCAPTCHA notice's (Google's terms, #22, #25),
  not theirs; their pages' own Terms of Service link is Atlassian's (above).
- **FAA** (#39, the status page): it links no terms, and it states none. A work of the US Government (17 U.S.C. § 105).
  **Not struck.**

## What is archived, and the budget

Bytes per poll from the probe's rows; stored = the depot's gzip. A year at 10 minutes is 52,560 polls; hourly, 8,760.

| endpoint | row | bytes | stored | cadence | stored a year |
|---|---|---|---|---|---|
| www.githubstatus.com/history.atom | #47 | 75,539 | 11,061 | hourly | 97 MB |
| status.claude.com/history.atom | #49 | 42,135 | 5,548 | hourly | 49 MB |
| status.alpaca.markets/history.atom | #51 | 60,838 | 9,032 | hourly | 79 MB |
| status.databento.com/history.atom | #53 | 38,718 | 6,231 | hourly | 55 MB |
| www.cloudflarestatus.com/api/v2/summary.json | #55 | 223,644 | 37,056 | hourly | 325 MB |
| www.cloudflarestatus.com/api/v2/incidents.json | #56 | 118,933 | 16,114 | hourly | 141 MB |
| status.cloud.google.com/incidents.json | #58 | 292,106 | 53,110 | hourly | 465 MB |
| nasstatus.faa.gov/api/airport-status-information | #40 | 2,488 | 835 | 10 min | 44 MB |
| **all** | | 854,401 an hour's set | 138,987 | | **≈ 1.25 GB stored** (≈ 7.6 GB as received) |

At 10 minutes for every endpoint the stored year is ≈ 7.3 GB, over the item's 2 GB. So the seven large endpoints are
slowed to hourly, as the item says (never dropped), and the FAA's snapshot, where a ground stop can start and end inside
an hour, stays at 10 minutes. The budget is read on stored bytes, what the disk holds (taken under the 10-31 filter;
reversible by an inbox block). Each feed and incident list carries every update's own timestamp, so an hourly read loses
only an edit made and replaced inside the hour. The cadence is the fetcher's knob (`every` in `STATUS_ENDPOINTS`).

## Not done here

No return read, no event taxonomy, no chokepoint entry, sentinel or freeze change (the item's fences).

## D857 (a), the operator's ruling 2026-11-15: AWS and Azure archived

The operator's chat answer 2026-11-15 ~17:25 ET, verbatim: "D855: yes" (relayed by the monitor session as
`data/inbox-answers/d855-aws-azure.md`): both struck sources are archived as personal non-commercial archiving, the
strike above waived by the operator's hand. Ledger lines for both already name this cadence; no line is added.

| endpoint | row | bytes | stored | cadence | stored a year |
|---|---|---|---|---|---|
| health.aws.amazon.com/public/currentevents | #37 | 246,112 (UTF-16 BE, BOM) | 24,457 | hourly | 214 MB |
| azure.status.microsoft/en-us/status/feed/ | #60 | 577 | 330 | 10 min | 17 MB |
| **all ten** | | | | | **≈ 1.48 GB stored** |

The shape check decodes AWS's body past its BOM (`decode`); the depot keeps the bytes as received.
