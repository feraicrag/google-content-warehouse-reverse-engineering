# Module inventory (hexdocs v0.4.0 api-reference)

The hexdocs api-reference page lists **162 model modules** visible on that single page. The client total is **2,596 modules / 14,014 attributes** (per Wikipedia + BeCited + commit stats).

Dominant prefixes observed:

- **Quality*** — largest family: Navboost Craps, NSR, RankEmbed, Timebased, PreviewSnippet, Authority, Spam*, Fringe, Vidya, and dozens more
- **PerDocData** and variants (PerDocDebugEvent, PremiumPerDocData, PhilPerDocData, SmartphonePerDocData, KaltixPerDocData, ...)
- **Indexing*** — Trawler, Alexandria, SegIndexer, rendering, canonicalization/WebMirror
- **SpamBrain*** — SpamBrainData and related
- **Anchors*** — Anchors, AnchorsAnchor, indexing_docjoiner_anchor_* (spam info, statistics, trusted info, surrounding context)
- **AssistantApi*** / **AppsPeople*** / **Youtube*** — non-search modules in the same client
- Remaining: Cloud API surface (Document AI Warehouse legacy + other GCP APIs bundled in the elixir client)

Full 2,596-module dump → Task 2 (HTML parse of hexdocs → JSON).
