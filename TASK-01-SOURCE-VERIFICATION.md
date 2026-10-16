# Task 1: Source Verification — COMPLETE

Verified against primary source: hexdocs.pm/google_api_content_warehouse/0.4.0

## Commits

| SHA | Date | Author | Files | Additions | Deletions | Description |
|-----|------|--------|-------|-----------|-----------|-------------|
| d7a637f | 2024-03-13 03:02 UTC | yoshi-code-bot | 2,596 | 178,764 | 0 | Addition of ContentWarehouse client (PR #11021) |
| 078b497 | 2024-05-07 | yoshi-code-bot | 2,423 | 7 | 164,707 | Removal of ContentWarehouse client (PR #11378) |

Parent of d7a637f: 35bfb58. Parent of 078b497: e6a95f9.
Repo archived 2026-06-30, read-only.

## Key Modules Verified

### QualityNavboostCrapsCrapsClickSignals (10 fields)
- absoluteImpressions (float) — host-level unsquashed impressions only
- badClicks (float)
- clicks (float)
- goodClicks (float)
- impressions (float)
- lastLongestClicks (float)
- unicornClicks (float) — clicks from Unicorn users
- unsquashedClicks (float) — not populated in current format
- unsquashedImpressions (float) — not populated in current format
- unsquashedLastLongestClicks (float)

### QualityNavboostCrapsCrapsData (22 fields)
- badClicks, clicks, goodClicks, impressions, lastLongestClicks (float)
- country (String) — two-letter uppercase country slice
- device (QualityNavboostCrapsCrapsDevice)
- features (list) — CrapsClickSignals for specific features
- language (String) — language slice
- lastLongestClicks (float) — clicks that were last and longest
- mobileData (self) — DO NOT USE, legacy
- mobileSignals (QualityNavboostCrapsCrapsClickSignals) — tier 1/2 mobile
- packedIpAddress (String) — for CrapsIpPrior
- patternLevel (integer) — 0=URL, higher=more general
- patternSccStats (QualityNavboostCrapsStatsWithWeightsProto)
- query (String)
- sliceTag (String) — arbitrary slice key
- squashed (QualityNavboostCrapsCrapsClickSignals) — not used yet
- unscaledIpPriorBadFraction (float) — prior to linear transform
- unsquashed (QualityNavboostCrapsCrapsClickSignals) — retuning rollout
- unsquashedMobileSignals (QualityNavboostCrapsCrapsClickSignals)
- url (String)
- voterTokenCount (integer) — lower bound on distinct users

### CompressedQualitySignals (30+ fields)
- siteAuthority (integer) — converted from quality_nsr.SiteAuthority, applied in Qstar
- babyPandaDemotion (integer) — from QualityBoost.rendered.boost
- babyPandaV2Demotion (integer) — replaces babyPandaDemotion
- pandaDemotion (integer) — encoding of Panda fields
- exactMatchDomainDemotion (integer) — from QualityBoost.emd.boost
- authorityPromotion (integer) — from QualityBoost.authority.boost
- unauthoritativeScore (integer) — Qstar signal
- scamness (integer) — 0-1023, Qstar signal
- crapsAbsoluteHostSignals (integer)
- crapsNewHostSignals (String)
- crapsNewPatternSignals (String)
- crapsNewUrlSignals (String)
- crapsUnscaledIpPriorBadFraction (integer)
- navDemotion (integer) — from QualityBoost.nav_demoted.boost
- pqData (integer) — encoded page-level PQ
- serpDemotion (integer) — applied in Qstar
- anchorMismatchDemotion (integer) — from QualityBoost.mismatched.boost
- ugcDiscussionEffortScore (integer) — times 1000 floored
- productReviewPPromotePage/DemotePage/PromoteSite/DemoteSite (integer)
- productReviewPUhqPage/ReviewPage (integer)
- topicEmbeddingsVersionedData (list of QualityAuthorityTopicEmbeddingsVersionedItem)
- experimentalQstarDeltaSignal (number) — NOT propagated to shards
- experimentalQstarSiteSignal (number) — NOT propagated to shards
- experimentalQstarSignal (number) — NOT propagated to shards
- experimentalNsrTeamData (QualityNsrExperimentalNsrTeamData)
- experimentalNsrTeamWsjData (list)
- nsrVersionedData (list) — deprecated, use nsr_data_proto
- nsrConfidence (integer) — deprecated
- nsrOverrideBid (number) — deprecated
- vlqNsr (integer) — deprecated, use nsr_data_proto
- lowQuality (integer) — from quality_nsr.NsrData
- pairwiseqScoringData (deprecated)
- pairwiseqVersionedData (list)
- pqDataProto (QualityNsrPQData)

### QualityNsrNsrData (40+ fields)
- nsr (number) — normalized site rank
- nsrVariance (number)
- nsrEpoch (String)
- nsrOverrideBid (number) — emergency override, >0.001 to take effect
- priorAdjustedNsr (list) — NSR minus prior
- nsrdataFromFallbackPatternKey (boolean)
- vlqNsr (number) — low-quality video NSR
- sitePr (number)
- siteLinkIn (number) — average site_link_in
- siteLinkOut (number) — aggregated url link out
- site2vecEmbedding (list of QualityNsrNsrDataEmbedding)
- site2vecEmbeddingEncoded (list of QualityNsrNsrDataEncodedEmbedding)
- siteChunk (String) — primary NSR sitechunk
- siteChunkSource (String)
- secondarySiteChunk (String)
- clusterId (integer) — Tundra ecosystem
- clusterUplift (QualityNsrNsrDataClusterUplift)
- chromeInTotal (number) — site-level Chrome views
- impressions (number) — site-level impressions
- titlematchScore (number) — how well titles match queries
- healthScore (number)
- shoppingScore (number)
- videoScore (number)
- ymylNewsV2Score (number)
- ugcScore (number)
- tofu (number) — site-level content quality predictor
- vlq (number) — video LQ model score
- articleScore (number)
- articleScoreV2 (number)
- chardEncoded (integer) — site-level chard score
- chardScoreEncoded (list)
- chardScoreVariance (list)
- chardVariance (number)
- clutterScore (number)
- clutterScores (list)
- directFrac (number)
- i18nBucket (integer)
- isCovidLocalAuthority (boolean)
- isElectionAuthority (boolean)
- isVideoFocusedSite (boolean) — >50% watch pages
- ketoVersionedData (list)
- language (integer)
- localityScore (number) — LocalAuthority component
- metadata (QualityNsrNsrDataMetadata)
- pnav (number)
- pnavClicks (number)
- racterScores (list)
- siteAutopilotScore (number)
- siteQualityStddev (number) — PQ rating stddev
- siteQualityStddevs (list)
- smallPersonalSite (number) — go/promoting-personal-blogs-v1
- spambrainLavcScore (number)
- spambrainLavcScores (list)
- url (String)
- versionedData (list)
- host (String)

NOTE: siteFocusScore and siteRadius are NOT in this module.

### QualityAuthorityTopicEmbeddingsVersionedItem (5 fields)
- pageEmbedding (String) — compressed page embedding
- siteEmbedding (String) — compressed site embedding
- siteFocusScore (number) — "Number denoting how much a site is focused on one topic"
- siteRadius (number) — "The measure of how far page_embeddings deviate from the site_embedding"
- versionId (integer)

Module description: Proto populated into shards and copied to superroot. Message storing a versioned TopicEmbeddings scores. This is copied from TopicEmbeddings in docjoins.

### PerDocData (115+ fields verified)
Key fields with descriptions:
- OriginalContentScore (integer) — 7-bit, 0-127, only pages with little content. Actual range 0-512. Encode/decode via quality_q2::OriginalContentUtil.
- homepagePagerankNs (integer) — page-rank of homepage, copied from cdoc.doc().pagerank_ns()
- homePageInfo (integer) — trust level enum: NOT_HOMEPAGE, NOT_TRUSTED, PARTIALLY_TRUSTED, FULLY_TRUSTED
- DocLevelSpamScore (integer) — 7-bit, 0-127
- GibberishScore (integer)
- KeywordStuffingScore (integer)
- SpamWordScore (integer)
- IsAnchorBayesSpam (boolean)
- ScaledSpamScoreEric/Yoram (integer) — 7-bit, 0-127
- ScaledExptSpamScoreEric/Yoram (integer)
- ScaledIndyRank (integer)
- ScaledExptIndyRank/2/3 (integer) — experimental
- ScaledLinkAgeSpamScore (integer)
- spamrank (integer)
- spambrainTotalDocSpamScore (number)
- spambrainData (SpamBrainData) — host-v1 sitechunk level scores
- spambrainDomainSitechunkData (SpamBrainData)
- spamMuppetSignals (SpamMuppetjoinsMuppetSignals) — hacked site signals
- spamCookbookAction (SpamCookbookAction)
- spamtokensContentScore (number) — used in SiteBoostTwiddler for UGC spam
- uacSpamScore (integer) — 7-bit, threshold 64
- trendspamScore (integer) — count of matching trendspam queries
- urlPoisoningData (UrlPoisoningData)
- pagerank/0/1/2 (number) — experimental, deprecated
- crawlPagerank (integer)
- toolbarPagerank (integer)
- domainAge (integer)
- hostAge (integer)
- lastSignificantUpdate (String) — UNIX timestamp from LSUSelector
- lastSignificantUpdateInfo (String)
- semanticDate (integer)
- semanticDateConfidence (integer) — deprecated
- semanticDateInfo (integer)
- timeSensitivity (integer)
- freshnessEncodedSignals (String)
- freshboxArticleScores (integer)
- datesInfo (String) — used in FreshnessTwiddler
- bodyWordsToTokensRatioBegin/Total (number)
- originalTitleHardTokenCount (integer)
- titleHardTokenCountWithoutStopwords (integer)
- commercialScore (number)
- TagPageScore (integer)
- scienceDoctype (integer) — <0 not science, 0 fully visible, >0 limited
- inNewsstand (boolean)
- isHotdoc (boolean)
- numUrls (integer) — alternate urls + 1
- onsiteProminence (integer)
- WhirlpoolDiscount (number)
- compressedQualitySignals (CompressedQualitySignals)
- nsrDataProto (QualityNsrNsrData) — stripped site-level signals
- nsrIsCovidLocalAuthority/ElectionAuthority/VideoFocusedSite (boolean)
- nsrSitechunk (String)
- biasingdata/2 (BiasingPerDocData/2)
- crowdingdata (CrowdingPerDocData)
- imagedata (ImagePerDocData)
- MobileData (MobilePerDocData)
- smartphoneData (SmartphonePerDocData)
- oceandata (OceanPerDocData)
- phildata (PhilPerDocData)
- kaltixdata (KaltixPerDocData)
- GroupsData (GroupsPerDocData)
- BlogData (BlogPerDocData)
- BookCitationData (BookCitationPerDocData)
- PremiumData (PremiumPerDocData)
- ToolBarData (ToolBarPerDocData)
- videodata (VideoPerDocData)
- videoLanguage (QualityVidyaVideoLanguageVideoLanguage)
- fireflySiteSignal (QualityCopiaFireflySiteSignal)
- brainloc (QualityGeoBrainlocBrainlocAttachment)
- countryInfo (CountryCountryAttachment)
- geodata (String)
- languages (list integer)
- rosettaLanguages (list String) — top two BCP-47 codes
- saftLanguageInt (list integer)
- pageTags (list integer)
- localizedCluster (IndexingDupsLocalizedLocalizedCluster)
- servingTimeClusterIds (IndexingDocjoinerServingTimeClusterIds)
- shingleInfo (ShingleInfoPerDocData)
- queriesForWhichOfficial (OfficialPagesQuerySet)
- productSitesInfo (QualityProductProductSiteData)
- launchAppInfo (QualityRichsnippetsAppsProtosLaunchAppInfoPerDocData)
- rsApplication (RepositoryAnnotationsRdfaRdfaRichSnippetsApplication)
- s3AudioLanguage (S3AudioLanguageS3AudioLanguage)
- mediaOrPeopleEntities (ImageQualitySensitiveMediaOrPeopleEntities)
- desktopInterstitials (IndexingMobileInterstitialsProtoDesktopInterstitials)
- noimageframeoverlayreason (integer)
- smearingMaxTotalOffdomainAnchors (integer)
- socialgraphNodeNameFp (String)
- knexAnnotation (SocialPersonalizationKnexAnnotation)
- v2KnexAnnotation (QualitySherlockKnexAnnotation)
- liveResultsData (WeboftrustLiveResultsDocAttachments)
- contentAttributions (ContentAttributions)
- extraData (Proto2BridgeMessageSet)
- crawlerIdProto (LogsProtoIndexingCrawlerIdCrawlerIdProto)
- eventsDate (list String)
- authorObfuscatedGaiaStr (list String)
- DEPRECATEDAuthorObfuscatedGaia (list String) — deprecated
- DEPRECATEDQuarantineWhitelist (boolean)
- QuarantineInfo (integer) — bitmask of QuarantineBits
- webrefEntities (RepositoryWebrefWebrefMustangAttachment)
- ymylHealthScore (integer) — requires pq-classifiers-announce join
- ymylNewsScore (integer)
- scaledSelectionTierRank (integer) — 0-32767, language normalized
- topPetacatTaxId (integer) — used in SiteboostTwiddler
- tundraClusterId (integer) — deprecated, use nsr_data_proto
- fringeQueryPrior (QualityFringeFringeQueryPriorPerDocData)
- travelGoodSitesInfo (QualityTravelGoodSitesData)
- asteroidBeltIntents (QualityOrbitAsteroidBeltDocumentIntentScores)
- appsLink (QualityCalypsoAppsLink)
- watchpageLanguageResult (WatchpageLanguageWatchPageLanguageResult)
- videoCorpusDocid (String)
- webmirrorEcnFp (String)
- urlAfterRedirectsFp (String)
- pageregions (String)
- compressedUrl (String)
- origin (integer)
- Event (list PerDocDebugEvent) — debug info
- scienceHoldingsIds (list String)

## Cross-Reference with Secondary Sources

| Field | iPullRank | SparkToro | Wikipedia | Primary Source |
|-------|-----------|-----------|-----------|----------------|
| siteAuthority | Yes | Yes | Yes | CompressedQualitySignals |
| goodClicks/badClicks/lastLongestClicks | Yes | Yes | Yes | QualityNavboostCrapsCrapsClickSignals |
| siteFocusScore | Yes | Yes | Yes (wrong module) | QualityAuthorityTopicEmbeddingsVersionedItem |
| siteRadius | Yes | Yes | Yes (wrong module) | QualityAuthorityTopicEmbeddingsVersionedItem |
| chromeInTotal | Yes | Yes | Yes | QualityNsrNsrData |
| smallPersonalSite | Yes | Yes | No | QualityNsrNsrData |
| homepagePagerankNs | Yes | No | No | PerDocData (not CompressedQualitySignals) |
| homePageInfo | Yes | No | No | PerDocData |
| hostAge | Yes | Yes | No | PerDocData |
| OriginalContentScore | Yes | No | No | PerDocData |
| contentEffort | Yes | No | No | NOT FOUND in hexdocs 0.4.0 |

## Corrections

1. Wikipedia states siteFocusScore and siteRadius live in QualityNsrNsrData. Incorrect. They live in QualityAuthorityTopicEmbeddingsVersionedItem (5 fields). QualityNsrNsrData has site2vecEmbedding/Encoded but not the focus/radius scores.
2. homepagePagerankNs and homePageInfo are in PerDocData, not CompressedQualitySignals. Some analyses conflated the two modules.
3. contentEffort was cited in multiple analyses but does not appear in any module verified against hexdocs 0.4.0. Status: unverified.

## Sources

- https://hexdocs.pm/google_api_content_warehouse/0.4.0/api-reference.html
- https://github.com/googleapis/elixir-google-api/commit/d7a637f4391b2174a2cf43ee11e6577a204a161e
- https://github.com/googleapis/elixir-google-api/commit/078b497fceb1011ee26e094029ce67e6b6778220
- https://en.wikipedia.org/wiki/2024_Google_Search_documentation_leak
- https://ipullrank.com/google-algo-leak
- https://sparktoro.com/blog/an-anonymous-source-shared-thousands-of-leaked-google-search-api-documents-with-me-everyone-in-seo-should-see-them/
