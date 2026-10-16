# Task 02 — Structured Extraction from Hexdocs 0.4.0

**Date:** 2026-10-16
**Source:** https://hexdocs.pm/google_api_content_warehouse/0.4.0/api-reference.html (primary, live)
**Method:** Direct page fetch of each module HTML page; field name, type, and description extracted verbatim.

## Modules Extracted

| Module | Fields | JSON file |
|---|---|---|
| PerDocData | 115 | perdocdata-fields.json |
| CompressedQualitySignals | 33 | compressed-quality-signals-fields.json |
| QualityNsrNsrData | 63 | quality-nsr-nsr-data-fields.json |
| QualityNavboostCrapsCrapsClickSignals | 10 | navboost-click-signals-fields.json |
| QualityNavboostCrapsCrapsData | 22 | navboost-craps-data-fields.json |
| QualityAuthorityTopicEmbeddingsVersionedItem | 5 | topic-embeddings-fields.json |

**Total fields extracted this pass: 248**

## Key Findings

1. **siteFocusScore / siteRadius location CORRECTED.** Wikipedia and multiple circulating analyses state these live in QualityNsrNsrData. Hexdocs 0.4.0 shows them in QualityAuthorityTopicEmbeddingsVersionedItem (5 fields: pageEmbedding, siteEmbedding, siteFocusScore, siteRadius, versionId). QualityNsrNsrData contains site2vecEmbedding and site2vecEmbeddingEncoded but NOT the focus/radius scores. The TopicEmbeddings module is populated into shards and copied to superroot; description: "Proto populated into shards and copied to superroot. Message storing a versioned TopicEmbeddings scores. This is copied from TopicEmbeddings in docjoins."

2. **siteAuthority CONFIRMED** in CompressedQualitySignals with literal description: "site_authority: converted from quality_nsr.SiteAuthority, applied in Qstar." Integer type, range context from scamness field (0-1023) suggests similar quantization.

3. **NavBoost click categories CONFIRMED** with internal engineering comments: goodClicks, badClicks, lastLongestClicks ("The number of clicks that were last and longest in related user queries"), unicornClicks ("The subset of clicks that are associated with an event from a Unicorn user"). absoluteImpressions note: "Thus far this field is only used for host level unsquashed impressions." unsquashedClicks/unsquashedImpressions: "This is not being populated for the current format - instead two instances of CrapsClickSignals (squashed/unsquashed) are used. We are migrating to the new format."

4. **CrapsData slicing CONFIRMED**: query, url, country ("The two-letter uppercase country slice"), language ("The language slice"), device, sliceTag ("arbitrary string for slicing by device type country locale"), patternLevel ("Level of pattern, more general patterns get higher values"), voterTokenCount ("lower bound on distinct users for privacy filtering"), packedIpAddress, unscaledIpPriorBadFraction (references craps-ip-prior.h and craps-penalty.cc).

5. **Experimental Q* fields in CompressedQualitySignals**: experimentalQstarSignal, experimentalQstarDeltaSignal, experimentalQstarSiteSignal — "This field is not propagated to shards. It is meant to be populated at serving time... The purpose of this field is to be read by an experimental Q* component, in order to quickly run LEs with new components. See go/0DayLEs." These are live-experiment fields, not shard-persisted.

6. **contentEffort STILL NOT FOUND.** Searched PerDocData, CompressedQualitySignals, QualityNsrNsrData, and related modules. Not present in hexdocs 0.4.0 verified modules. Remains UNCONFIRMED. Circulating analyses mention it; primary source does not show it in the modules checked.

7. **homepagePagerankNs / homePageInfo CONFIRMED in PerDocData** (not CompressedQualitySignals as some analyses implied).

8. **New CompressedQualitySignals fields not previously highlighted**: ugcDiscussionEffortScore ("UGC page quality signals. Times 1000 and floored"), productReviewPPromotePage/DemotePage/PromoteSite/DemoteSite/UhqPage/ReviewPage, pairwiseqScoringData ("Deprecated and unused field"), nsrVersionedData (deprecated, use nsr_data_proto), nsrConfidence (deprecated, use nsr_variance), lowQuality ("S2V low quality score... applied in Qstar").

## Discrepancies vs Circulating Analyses

- siteFocusScore/siteRadius: Wikipedia says QualityNsrNsrData; hexdocs says QualityAuthorityTopicEmbeddingsVersionedItem.
- contentEffort: mentioned in analyses, absent from hexdocs 0.4.0 modules verified.
- Module count: api-reference page shows 162 visible model modules; commit stats say 2,596 modules / 14,014 attributes. The 162 is the HTML-rendered subset.

## Next Steps (Task 03)

- Parse full api-reference.html for all 2,596 module names.
- Bulk-fetch each module page and extract fields programmatically.
- Cross-reference against patent numbers and DOJ testimony.
- Build the master 3-column table: leak field → patent → practical implication.