# Corrections to Circulating Analyses

## 1. siteFocusScore and siteRadius module location

Wikipedia and multiple secondary analyses state that siteFocusScore and siteRadius live in QualityNsrNsrData. This is incorrect.

Verified location: QualityAuthorityTopicEmbeddingsVersionedItem (5 fields).

QualityNsrNsrData contains site2vecEmbedding and site2vecEmbeddingEncoded but does not contain siteFocusScore or siteRadius.

## 2. homepagePagerankNs and homePageInfo location

Some analyses place these in CompressedQualitySignals. They are in PerDocData.

homepagePagerankNs: integer, page-rank of homepage copied from cdoc.doc().pagerank_ns().
homePageInfo: integer, trust level enum (NOT_HOMEPAGE, NOT_TRUSTED, PARTIALLY_TRUSTED, FULLY_TRUSTED).

## 3. contentEffort

Cited in multiple analyses as an LLM-based effort estimation field. Not found in any module verified against hexdocs v0.4.0. Status: unverified against primary source.

## 4. Module count

Commit d7a637f added 2,596 files. Wikipedia and SparkToro cite 2,596 modules and 14,014 attributes. Hexdocs API reference page shows 162 model modules visible on the index page; the full client contains 2,596 modules.

## Sources

- hexdocs v0.4.0 (primary)
- Wikipedia 2024 Google Search documentation leak (secondary, contains error)
- iPullRank analysis (secondary)
- SparkToro analysis (secondary)
