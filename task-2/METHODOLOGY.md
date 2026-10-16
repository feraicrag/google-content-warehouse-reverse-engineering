# Task 02 — Methodology (Reproducible)

## Source

- Hexdocs 0.4.0: https://hexdocs.pm/google_api_content_warehouse/0.4.0/api-reference.html
- Base URL pattern: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.{ModuleName}.html
- Commit range: d7a637f (add, 2024-03-13) → 078b497 (remove, 2024-05-07); repo archived 2024-06-30.

## Extraction Protocol

1. Fetch module HTML page directly (no JS rendering needed; hexdocs is static).
2. Locate the "Fields" section (table or definition list).
3. For each row: field name (backtick-wrapped identifier), type (e.g. integer(), float(), String.t, list(...)), description (literal text or "(no description provided)" / "(empty description)").
4. Record verbatim. Do not paraphrase descriptions in the JSON; paraphrase only in markdown analysis files.
5. Count fields per module; flag deprecated/unused fields explicitly.
6. Cross-check module names against the 162 visible on api-reference page vs 2,596 in commit stats.

## Tools Used

- browse_page (LLM summarizer over fetched HTML) for field extraction.
- github push tools for versioned commits.
- No local clone of the Elixir client; hexdocs is the external cache.

## Limitations

- Hexdocs 0.4.0 may not capture every proto revision; some fields may exist in other versions or in the raw .proto files not rendered as separate HTML pages.
- The 162-module api-reference listing is an HTML subset; bulk extraction of all 2,596 requires parsing the full module index or the GitHub tarball of commit d7a637f.
- Descriptions are engineer comments, not guarantees of current production weight.

## Verification Checklist

- [x] PerDocData fields extracted
- [x] CompressedQualitySignals fields extracted
- [x] QualityNsrNsrData fields extracted (63)
- [x] QualityNavboostCrapsCrapsClickSignals fields extracted (10)
- [x] QualityNavboostCrapsCrapsData fields extracted (22)
- [x] QualityAuthorityTopicEmbeddingsVersionedItem fields extracted (5)
- [x] Cross-reference table built (leak → patent → DOJ → implication)
- [x] Criterion defined for active vs stored vs experiment vs deprecated
- [ ] Bulk extraction of remaining ~2,590 modules (Task 03)