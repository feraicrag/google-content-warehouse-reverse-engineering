# Google Content Warehouse API Leak — Reverse Engineering

Primary-source reverse engineering of Google's Content Warehouse API leak (March–May 2024).

## Status

- [x] Task 1 — source verification + field extraction of priority modules
- [x] Task 2 — structured extraction of PerDocData, CompressedQualitySignals, QualityNsrNsrData, NavBoost, TopicEmbeddings
- [x] Task 3 — additional modules (CompositeDoc, Anchors/AnchorsAnchor, QualityNsrPQData, SpamBrainData, SyntacticDate, AnchorSpamInfo)
- [x] Task 4 — leak-patent-DOJ cross-map + ranking roadmap

## Key corrections

- **contentEffort confirmed** in `QualityNsrPQData` as `list(QualityNsrVersionedFloatSignal)`, description: "LLM-based effort estimation for article pages (see landspeeder/4311817)."
- siteFocusScore / siteRadius live in `QualityAuthorityTopicEmbeddingsVersionedItem`, not QualityNsrNsrData.
- homepagePagerankNs / homePageInfo live in PerDocData.

## Primary sources

- Hexdocs v0.4.0: https://hexdocs.pm/google_api_content_warehouse/0.4.0/api-reference.html
- Addition commit: https://github.com/googleapis/elixir-google-api/commit/d7a637fceb1011ee26e094029ce67e6b6778220
- Removal commit: https://github.com/googleapis/elixir-google-api/commit/078b497fceb1011ee26e094029ce67e6b6778220

## Verified modules (hexdocs 0.4.0)

- PerDocData
- CompressedQualitySignals
- QualityNavboostCrapsCrapsData
- QualityNavboostCrapsCrapsClickSignals
- QualityNsrNsrData
- QualityAuthorityTopicEmbeddingsVersionedItem
- CompositeDoc
- DocProperties
- Anchors / AnchorsAnchor
- SpamBrainData
- QualityNsrPQData (contentEffort)
- RepositoryWebrefWebrefMustangAttachment
- QualityTimebasedSyntacticDate
- IndexingDocjoinerAnchorSpamInfo
- IndexingDocjoinerAnchorPhraseSpamInfo

See `task-*/` directories for field-level dumps.
