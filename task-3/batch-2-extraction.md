# Task 3 — Batch 2: Module Extraction from hexdocs 0.4.0

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/api-reference.html
Date extracted: 2026-10-16

## Verified modules (page exists, fields extracted)

### QualityTimebasedLastSignificantUpdate (4 fields)
- `adjustmentInfo` String/struct — stored only for debugging; consult dates@ team before depending
- `date` String — LastSignificantUpdate as UNIX timestamp in seconds. New signal (go/lsu-dd) from LSU Selector V2, falling back to legacy V1 if HIGH_PRECISION signal does not exist. Use `source` field to determine origin.
- `dateUnreliabilityInfo` struct — no detailed description
- `source` String — the source the signal comes from

### QualityRankembedMustangMustangRankEmbedInfo (7 fields)
- `additionalFixedPointEncodings` list(String) — each element same scheme as fixed_point_encoding; see go/rankembed-astro-rule-set-dd
- `compressedDocumentEmbedding` struct — each uint64 encodes 8 8-bit values for quantized document embedding
- `fixedPointEncoding` String — replaces the 3 per-encoding-type fields; encoding type and embedding type are part of the encoding, stored in first byte; remaining bytes shifted by 1
- `scaledFixedPoint4Encoding` String — byte[0]: version, bytes[1..4]: scalar, bytes[5..]: values one byte per 2 values
- `scaledFixedPoint8Encoding` String — byte[0]: version, bytes[1..4]: scalar, bytes[5..]: values one byte per value
- `scaledShiftedFixedPoint4Encoding` String — byte[0]: version, bytes[1..4]: scalar, bytes[5..8]: shift, bytes[9..]: values one byte per 2 values
- `versionAndImprovInfo` integer — first 7 bits encode version, then each chunk of 5 bits encodes index of a potential improv query (lsb to msb). As of cl/270008220 only contains version info.

### IndexingDocjoinerAnchorSpamInfo (19 fields)
- `anchorEnd` integer — end date of the last anchor of the document
- `anchorFraq` number — ratio of spam demoted period to all anchor period
- `anchorStart` integer — start date of the first anchor of the document
- `demoted` integer — number of anchors demoted
- `demotedAll` boolean — whether all anchors in the period were demoted or only spam-classified ones
- `demotedEnd` integer — end date of the demotion period
- `demotedStart` integer — start date of the demotion period
- `phraseCount` number — number of spam phrases found in anchors among unique domains
- `phraseDays` number — number of days over which 80% of these phrases were discovered
- `phraseFraq` number — fraction of spam phrases relative to all anchors of the document
- `phraseRate` number — average daily rate of spam anchor discovery
- `processed` integer — total number of processed anchors
- `sampled` boolean — whether anchors were sampled during the observation period
- `sources` list(struct) — detailed info about trusted sources and match computation (populated only when --anchorspam_penalizer_debug=true)
- `spamDebugInfo` String — additional debug info about spam probability computation
- `spamPenalty` number — combined penalty applied for anchor demotion
- `spamProbability` number — predicted probability that the anchor text is spam
- `trustedDemoted` integer — number of trusted anchors used in spam probability computation
- `trustedExamples` String — examples of trusted sources
- `trustedMatching` integer — number of trusted anchors whose anchor text matches spam terms
- `trustedTarget` boolean — indicates whether the URL is a trusted source
- `trustedTotal` integer — total number of trusted sources for this URL

### SpamBrainData (2 fields)
- `site` String — Sitechunker site granularity for this result
- `versionedData` list(SpamBrainScore) — versioned scores of SB classifiers

### SpamBrainScore (3 fields)
- `modelName` String — no description
- `sbScore` number — the value corresponding to this version
- `versionId` integer — version id derived from epoch; larger number means newer score

### QualityTimebasedSyntacticDate (from batch 1, 13 fields — retained for reference)
- date, bylineDate, precisionMark, trustSyntacticDateInRanking, useAsBylineDate, useInTimeZoneGuessingMode, useRangeInsteadOfDateForRestrict, syntacticDateNotForRestrict, fromExplicitTimeZone, timeZoneOffsetSeconds, info, position, daterange

## 404 log — guessed module names that do NOT exist in hexdocs 0.4.0

These names were inferred from blog analyses and DOJ materials, not from the hexdocs index. All returned 404:

1. QualityTwiddlerCrapsCrapsData
2. IndexingUrlPattern
3. QualityBoost
4. QualityFreshnessFreshnessData
5. GlueUserBehaviorSignals
6. QualitySiteQualityScore
7. QualityOriginalContentScore
8. QualityPreviewSnippet
9. QualityNsrSite2vecEmbedding
10. QualityTimebasedSyntacticDateInfo
11. RepositoryWebrefWebrefEntityMetadata
12. QualityNavboostCrapsCrapsIpPrior
13. IndexingTrawler

IMPORTANT: This means several names circulating in SEO analyses (QualityBoost, QualitySiteQualityScore, QualityOriginalContentScore, GlueUserBehaviorSignals, IndexingTrawler) are NOT directly verifiable as standalone modules in hexdocs 0.4.0. They may live under different names, be nested inside other protos, or be from a different API version. The hexdocs client only exposes what the Elixir generator emitted.

## API reference prefix inventory (from browse of api-reference.html)

Modules found grouped by prefix (partial — page is long, summarizer returned segments):

- Indexing*: IndexingDupsComputedLocalizedAlternateNamesLocaleEntry, IndexingBadSSLCertificate
- Anchor*: Anchors, AnchorsAnchor, AnchorsAnchorSource, AnchorsRedundantAnchorInfo
- Navboost*: CountryMetroNBFeature
- Site*: ClassifierPornSiteData, ClassifierPornSiteDataVersionedScore
- Query*: ClassifierPornQueryClassifierOutput, ClassifierPornQueryMultiLabelClassifierOutput, ClassifierPornQueryStats, ExtraSnippetInfoResponse (+MatchInfo, QuerySubitem, Tidbit, TidbitAnchorInfo)
- Click*: CountryClickDistribution, CountryClickDistributionItem
- Content*: ContentAttributions, ContentAttributionsOutgoingAttribution, GDocumentBaseContent, GDocumentBaseOriginalContent
- Snippet*: GenericSnippetResponse
- Video*: DrishtiVesperMovingThumbnail (+ScoreComponents), DrishtiVesperThumbnail, DrishtiVesperThumbnailQualityScore, DrishtiVesperUserReportHumanLabel, DrishtiVesperUserReportModelScore, DrishtiVesperUserReportUserReportedThumbnail, DrishtiVesperVideoThumbnail
- Image*: CommerceDatastoreImageDeepTags, CommerceDatastoreImageDeepTagsModelOutput, ContentAwareCropsIndexing, DeepCropIndexing, DeepCropPixels, FaceIndexing
- Data*: BlobstoreBlobRef, CommerceDatastoreDeepTag, CommerceDatastoreImageDeepTagsModelOutput, CorpusSelectionInfo, Geostore* (many address/geometry/feature protos)
- Knowledge*: FreebaseCitation, FreebaseId, FreebaseLatLong, FreebaseMeasurement, FreebaseMeasurementUnit, FreebaseNestedStruct, FreebasePropertyValue, FreebaseTopic, FreebaseValue
- Assistant*: AssistantVerticalsHomeautomationProto* (device targeting, smart home), AttentionalEntities* (mention properties, semantic role, spatial properties, surface form), BlueGingerClientVisibleProto*, ChatBotPlatform*, ClassifierPorn*
- Apps*: AppsDynamite*, AppsPeopleOzExternalMergedpeopleapi* (large people API surface)

Key observation: the api-reference page does NOT surface Quality*, PerDocData, CompressedQualitySignals, QualityNsr*, QualityNavboost*, QualityRankembed*, SpamBrain*, CompositeDoc, DocProperties as top-level listed prefixes in the segments returned. They are reachable by direct URL construction (GoogleApi.ContentWarehouse.V1.Model.<Name>.html) but not browsable from the index page segments. This suggests the hexdocs page is very long and the summarizer only captured portions, OR the index uses a different grouping.

## Findings for task 3

1. RankEmbed module CONFIRMED with full field list including go/ internal doc links (go/rankembed-astro-rule-set-dd, cl/270008220). This is the neural embedding layer for ranking.
2. AnchorSpamInfo CONFIRMED with 19 fields including spamProbability, spamPenalty, phraseRate, phraseFraq, phraseDays — this is the anchor spam velocity/pattern detection the patents describe (US7346839B2 historical data, phrase-based spam).
3. SpamBrainData + SpamBrainScore CONFIRMED — versioned classifier scores with epoch-derived versionId.
4. LastSignificantUpdate CONFIRMED — with explicit note that it is the NEW signal from LSU Selector V2 (go/lsu-dd), falling back to legacy V1. Source field tells you origin.
5. 13 guessed names 404'd. The blog-circulated names are unreliable as direct module names.
6. CompositeDoc architecture from batch 1 still stands: PerDocData -> compressedQualitySignals -> CompressedQualitySignals; PerDocData -> nsrDataProto -> QualityNsrNsrData; CompositeDoc.anchors -> Anchors; CompositeDoc.doc -> PerDocData.

## Next for task 3

- Batch 3: try alternate name patterns for 404'd modules (e.g., QualityBoost* variants, Glue* variants, IndexingTrawler* variants)
- Batch 4: extract Quality* subfamily modules systematically
- Batch 5: extract Indexing* subfamily
- Then: build master glossary JSON of all found modules
- Then: cross-reference against patents (task 4)