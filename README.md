# Finance Brain — Forward Research & Operations Record

Public track record for a solo-operator, paper-only market research platform.
The product here is **process, not returns**: pre-registered hypotheses, one-shot
holdout gates, and a denominator that includes every kill.

## What's in this repo

- `record/claims.json` — the research-claims register: every governed hypothesis
  program ever run, with status, verdict, and pre-registration commit hashes.
  Kills included; that is the point. Updated when program state changes.
- `record/ops/YYYY-MM-DD.json` — weekly operations snapshot (cron health of the
  ingest/monitoring substrate: OK/LATE/SILENT per job).
- `record/anchors/YYYY-MM-DD.json` — weekly anchor: private-mirror HEAD commit,
  provenance manifest sha256, and sha256 hashes of the weekly database snapshots.
- `strategies/` — validated strategies panel. **Currently empty, honestly**: a
  strategy appears only after a pre-registered confirmatory PASS on virgin
  holdout data.

## Verification protocol

1. Every commit in this repo is timestamped by GitHub at push time. A claim in
   `record/claims.json` is only as old as the earliest public commit containing it.
2. Research work lives in a **private mirror**
   (`JimmyNewtron711/finance-brain`), pushed daily, so every pre-registration
   commit hash cited here is anchored off-box within 24 hours of creation.
   `record/anchors/*.json` publishes the mirror's `main` HEAD weekly — the hash
   chain makes silent history rewrites detectable.
3. A verifying party (allocator, prop firm, reviewer) can request read access to
   the private mirror and check that: cited pre-registration commits predate the
   runs they govern, verdict reports match the register, and the anchor hashes
   published here match the mirror's history.
4. Database snapshot hashes in `record/anchors/*.json` correspond to weekly
   `VACUUM INTO` snapshots retained locally; on request their contents can be
   verified against the published sha256s.

**Kill condition this record is built to satisfy: no claim is publishable after
its outcome is known.** Claims enter the register with pre-registration hashes
before runs execute; anchoring is automatic and daily.

## Provenance

Bundles are produced by `scripts/forward-record.mjs` in the private repo
(weekly cron), which refuses to publish on stale or missing inputs.
