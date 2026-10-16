# Google Content Warehouse API Leak — Reverse Engineering

Primary-source reverse engineering of Google's Content Warehouse API leak (March–May 2024).

**Task 1 of 100: Source verification & field extraction — COMPLETE.**

## What this is

On March 13, 2024, Google's automated bot `yoshi-code-bot` accidentally regenerated and pushed internal documentation for Google Search's Content Warehouse API to the public repo `googleapis/elixir-google-api` (commit `d7a637f...`, PR #11021). It was removed on May 7, 2024 (commit `078b497...`). By then, hexdocs had cached the full schema: **2,596 modules, 14,014 attributes** (google_api_content_warehouse v0.4.0, Apache 2.0).

This project verifies every circulating claim against that primary source, field by field.

## Repo layout

- `task-1/` — Task 1 deliverables (source verification, full field extraction, cross-reference)
  - `SOURCE_VERIFICATION.md` — commits, dates, authors, stats
  - `PERDOC_DATA.md` — complete PerDocData field list (70+ fields, verbatim from hexdocs)
  - `COMPRESSED_QUALITY_SIGNALS.md` — complete CompressedQualitySignals
  - `QUALITY_NSR_NSR_DATA.md` — complete QualityNsrNsrData (42 fields)
  - `NAVBOOST_CRAPS.md` — QualityNavboostCrapsCrapsData (22 fields) + CrapsClickSignals (10 fields)
  - `TOPIC_EMBEDDINGS.md` — QualityAuthorityTopicEmbeddingsVersionedItem (siteFocusScore, siteRadius)
  - `MODULE_INVENTORY.md` — module prefix inventory from hexdocs api-reference
  - `CROSS_REFERENCE.md` — leak fields ↔ patents ↔ DOJ testimony ↔ circulating analyses
  - `CORRECTIONS.md` — errors found in Wikipedia and other circulating summaries
  - `UNCONFIRMED.md` — fields mentioned in analyses but NOT found in hexdocs v0.4.0
- `tasks/` — the 100-task roadmap
- `notes/` — working notes

## Key findings (Task 1)

1. **siteAuthority is real** — integer in CompressedQualitySignals, literal description: "converted from quality_nsr.SiteAuthority, applied in Qstar".
2. **NavBoost click taxonomy confirmed** — goodClicks, badClicks, lastLongestClicks, unsquashedClicks, unicornClicks, impressions, absoluteImpressions (host-level only), squashed/unsquashed nesting.
3. **siteFocusScore and siteRadius do NOT live in QualityNsrNsrData** — they live in `QualityAuthorityTopicEmbeddingsVersionedItem` (5 fields: pageEmbedding, siteEmbedding, siteFocusScore, siteRadius, versionId). Wikipedia's claim that they are in NSR data is incorrect per hexdocs v0.4.0.
4. **homepagePagerankNs and homePageInfo are in PerDocData**, not CompressedQualitySignals.
5. **contentEffort** (LLM-based effort estimation) — mentioned in circulating analyses, NOT found in any module opened in hexdocs v0.4.0. Marked unconfirmed.
6. Full PerDocData extraction: 70+ fields including spam scores, PageRank variants, freshness dates, OriginalContentScore, authorship, and deprecated fields.

## Primary sources

- Hexdocs v0.4.0: https://hexdocs.pm/google_api_content_warehouse/0.4.0/api-reference.html
- Addition commit: https://github.com/googleapis/elixir-google-api/commit/d7a637fceb1011ee26e094029ce67e6b6778220
- Removal commit: https://github.com/googleapis/elixir-google-api/commit/078b497fceb1011ee26e094029ce67e6b6778220
- iPullRank (Mike King): https://ipullrank.com/google-algo-leak
- SparkToro (Rand Fishkin): https://sparktoro.com/blog/an-anonymous-source-shared-thousands-of-leaked-google-search-api-documents-with-me-everyone-in-seo-should-see-them/

## Status

- [x] Task 1 — source verification + field extraction
- [ ] Task 2 — parse hexdocs HTML, dump all 2,596 modules to JSON
- [ ] Task 3 — patent cross-reference table
- [ ] ... (tasks 4–100)

## License

Hexdocs content is Apache 2.0 (Google's client library). Analysis and synthesis in this repo: all rights reserved by the author.
