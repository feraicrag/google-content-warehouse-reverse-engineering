# Priority Modules Extraction — hexdocs 0.4.0

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/
Date: 2026-10-18

## CompressedQualitySignals (Next id: 43)

Per-doc signals compressed for Mustang and TeraGoogle. Used in preliminary scoring. Limited serving memory.

Key fields:
- `siteAuthority` integer — converted from quality_nsr.SiteAuthority, applied in Qstar
- `pandaDemotion` integer — encoding of Panda fields from SiteQualityFeatures proto
- `babyPandaDemotion` integer — converted from QualityBoost.rendered.boost
- `babyPandaV2Demotion` integer — new BabyPanda demotion on top of Panda
- `authorityPromotion` integer — converted from QualityBoost.authority.boost
- `navDemotion` integer — converted from QualityBoost.nav_demoted.boost
- `exactMatchDomainDemotion` integer — converted from QualityBoost.emd.boost (10-bit encoding of [0,1] float)
- `anchorMismatchDemotion` integer — converted from QualityBoost.mismatched.boost
- `serpDemotion` integer — applied in Qstar
- `scamness` integer — Scam model score, 0-1023, used in Qstar
- `unauthoritativeScore` integer — used in Qstar
- `lowQuality` integer — S2V low quality, converted from quality_nsr.NsrData
- `productReviewPUhqPage` integer — possibility of high quality review page
- `productReviewPReviewPage` integer — possibility of review page (go/pr-boosts)
- `ugcDiscussionEffortScore` integer — UGC page quality (x1000 floored)
- `topicEmbeddingsVersionedData` list(QualityAuthorityTopicEmbeddingsVersionedItem) — versioned TopicEmbeddings for superroot/scorers
- `pqDataProto` QualityNsrPQData — stripped page-level signals
- `experimentalQstarSignal` / `experimentalQstarDeltaSignal` / `experimentalQstarSiteSignal` — NOT propagated to shards; populated at serving time for LEs (go/0DayLEs)
- `experimentalNsrTeamData` / `experimentalNsrTeamWsjData` — populated by web-signal-joins, LEs only
- `crapsNewUrlSignals` / `crapsNewHostSignals` / `crapsNewPatternSignals` — do not access directly; use craps-lossy-compression.h
- `nsrVersionedData` / `nsrConfidence` / `vlqNsr` — DEPRECATED, use nsr_data_proto instead

## QualityNavboostCrapsCrapsClickSignals

Click/impression signals for craps. Tag numbers match original CrapsData.

Fields:
- absoluteImpressions float — host-level unsquashed impressions only; incompatible with compressed click-ratios
- badClicks float
- clicks float
- goodClicks float
- impressions float
- lastLongestClicks float
- unicornClicks float — subset of clicks from Unicorn users
- unsquashedClicks float — migrating; currently two instances (squashed/unsquashed) used
- unsquashedImpressions float
- unsquashedLastLongestClicks float

## QualityNavboostCrapsCrapsData (NEXT TAG: 28)

- badClicks, clicks, goodClicks, impressions, lastLongestClicks float
- country String — two-letter uppercase (US, FR, BR)
- language String — en, fr, pt-BR
- device QualityNavboostCrapsCrapsDevice — interface + OS slice
- features list(QualityNavboostCrapsFeatureCrapsData) — CrapsClickSignals for specific features (mobile, US, metro)
- mobileSignals QualityNavboostCrapsCrapsClickSignals — tier 1/2 mobile interfaces from QSessions
- squashed / unsquashed QualityNavboostCrapsCrapsClickSignals — future nesting; unsquashed for retuning rollout
- lastLongestClicks float — clicks that were last AND longest in related user queries
- unscaledIpPriorBadFraction float — IP prior before linear transform (craps-penalty.cc)
- voterTokenCount integer — lower bound on distinct users (privacy filtering)
- patternLevel integer — 0 for exact URL, higher for more general patterns
- sliceTag String — arbitrary string for slicing by device/country/locale; aggregated separately

## QualityNsrNsrData (Next ID: 63)

NOTE: When adding a field to be propagated to Raffia, check NsrPatternSignalSpec.

Key fields:
- nsr number — the NSR score itself
- siteAuthority (via CompressedQualitySignals) — applied in Qstar
- site2vecEmbedding list(QualityNsrNsrDataEmbedding) — full embeddings
- site2vecEmbeddingEncoded list — compressed for superroot
- siteFocusScore / siteRadius — in QualityAuthorityTopicEmbeddingsVersionedItem (not here)
- chardEncoded integer — site-level content quality predictor
- tofu number — site-level tofu score (content predictor)
- titlematchScore number — how well titles match queries
- localityScore number — locality component of LocalAuthority (go/pq-localauthority)
- smallPersonalSite number — promotion score (go/promoting-personal-blogs-v1)
- isVideoFocusedSite boolean — >50% watch pages, not on known video hosts
- isElectionAuthority boolean — go/election-authority
- isCovidLocalAuthority boolean — go/covid-local-authority
- clusterId integer — site clusters for Tundra experiments
- clusterUplift QualityNsrNsrDataClusterUplift — local/small site uplift arms
- nsrOverrideBid number — emergency override in Q* (must be >0.001)
- priorAdjustedNsr list — NSR minus prior (above/below average in slice)
- spambrainLavcScore number — SpamBrain LAVC as of July 2022 (go/cloverfield-lavc-deck)
- racterScores list — site-level AGC classification (go/project-racter-overview)
- siteChunk String — primary NSR sitechunk (usually HOST_LEVEL_V3)
- secondarySiteChunk String — more granular when present
- nsrdataFromFallbackPatternKey boolean — data from average of other host chunks

## QualityAuthorityTopicEmbeddingsVersionedItem

Proto populated into shards and copied to superroot. Versioned TopicEmbeddings.

- pageEmbedding String
- siteEmbedding String — compressed site/page embeddings
- siteFocusScore number — how much a site is focused on one topic
- siteRadius number — how far page_embeddings deviate from the site_embedding
- versionId integer

NOTE: siteFocusScore and siteRadius live HERE, not in QualityNsrNsrData. Corrects earlier Wikipedia/blog claims.

## QualityNsrPQData (Next id: 22)

- contentEffort list(QualityNsrVersionedFloatSignal) — LLM-based effort estimation for article pages (landspeeder/4311817). CONFIRMED.
- chard integer — URL-level chard prediction
- keto list — Keto score
- rhubarb list — Site-URL delta quality via Rhubarb model (go/rhubarb-dd)
- predictedDefaultNsr list — Goldmine NSR default predictor
- numOffdomainAnchors number — offdomain anchors seen by NSR pipeline
- deltaSubchunkAdjustment number — page-level deltaNSR from subchunks
- tofu number — URL-level tofu
- vlq number — URL-level VLQ model score

## CompositeDoc (Next id: 194)

Protocol record collecting all document information. Consult go/dj-explorer. New fields require go/dj-new-field ticket.

Key refs:
- perDocData → PerDocData
- anchors → Anchors (non-personal)
- anchorStats → IndexingDocjoinerAnchorStatistics
- qualitysignals → CompositeDocQualitySignals
- properties → DocProperties
- doc → GDocumentBase
- syntacticDate → QualityTimebasedSyntacticDate
- url is optional/usually missing; prefer CompositeDoc::doc::url

## AnchorsAnchor

sourceType integer — quality of source page, correlated with index tier:
- TYPE_HIGH_QUALITY: base documents
- TYPE_MEDIUM_QUALITY: medium quality (~supplemental)
- TYPE_LOW_QUALITY: low quality (~blackhole)
- TYPE_FRESHDOCS: treated as HIGH_QUALITY for importance

locality integer — quality measure with bucket (see quality/anchors/definitions.h)
pagerankWeight number — weight for pageranker linkmaps
origText String — original text with capitalization/punctuation
text String — space-delimited words (CJK unsegmented)
experimental boolean — if true, not for serving
firstseenDate integer — days past Dec 31 1994 23:00 UTC
