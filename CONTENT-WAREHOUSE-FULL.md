# Google Content Warehouse API - Ranking Signals Extraction
# Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/api-reference.html
# Extracted: 2026-10-18

## Status
Total modules in API: 162
Ranking-relevant modules fully extracted: 6

---

## QualityNsrNsrData (Site-level)
chromeInTotal, titlematchScore, site2vecEmbedding, smallPersonalSite, isVideoFocusedSite, chardVariance, clusterId, nsr, localityScore, siteChunk, tofu, siteLinkOut, impressions, vlq, spambrainLavcScore, articleScore, ymylNewsV2Score, isElectionAuthority, sitePr, priorAdjustedNsr

## QualityNavboostCrapsCrapsClickSignals
absoluteImpressions, badClicks, clicks, goodClicks, impressions, lastLongestClicks, unicornClicks, unsquashedClicks, unsquashedImpressions, unsquashedLastLongestClicks

## CompressedQualitySignals
siteAuthority, exactMatchDomainDemotion, lowQuality, navDemotion, babyPandaV2Demotion, authorityPromotion, scamness, pandaDemotion, unauthoritativeScore, productReviewPReviewPage, topicEmbeddingsVersionedData, vlqNsr

## QualityNsrPQData (Page-level)
contentEffort (LLM-based effort estimation), chard, keto, predictedDefaultNsr, rhubarb, tofu, vlq, numOffdomainAnchors, deltaSubchunkAdjustment

## PerDocData
lastSignificantUpdate (UNIX timestamp), OriginalContentScore (0-127), uacSpamScore (threshold 64), spamtokensContentScore, ymylHealthScore, webrefEntities, spambrainData, homepagePagerankNs

## Google Discover (2026)
- pCTR model: title, image size, age, past CTR
- Freshness: 1-7 days strongest, 30+ decline
- Image: >=1200px for large cards
- Blocking: nopagereadaloud, notranslate
- Feb 2026 update: local relevance, reduced clickbait, topic expertise
- Pipelines: editorial, news urgency, trends, local, social/video
