# QualityNsrNsrData — complete field extraction (hexdocs v0.4.0)

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityNsrNsrData.html

42 fields.

- `nsr`
- `nsrVariance`
- `nsrEpoch`
- `nsrOverrideBid`
- `priorAdjustedNsr`
- `nsrdataFromFallbackPatternKey`
- `vlqNsr`
- `sitePr`
- `siteLinkIn` / `siteLinkOut`
- `site2vecEmbedding` (string)
- `site2vecEmbeddingEncoded` (string) — comment: encoded used in superroot because full embedding is too large
- `siteChunk` / `siteChunkSource` / `secondarySiteChunk`
- `clusterId`
- `clusterUplift`
- `chromeInTotal`
- `impressions`
- `titlematchScore`
- `healthScore`
- `shoppingScore`
- `videoScore`
- `ymylNewsV2Score`
- `ugcScore`
- `tofu`
- `vlq`
- `articleScore` / `articleScoreV2`
- `chardEncoded` / `chardScoreEncoded` / `chardScoreVariance` / `chardVariance`
- `clutterScore` / `clutterScores`
- `directFrac`
- `i18nBucket`
- `isCovidLocalAuthority`
- `isElectionAuthority`
- `isVideoFocusedSite`
- `ketoVersionedData`
- `language`
- `localityScore`
- `metadata`
- `pnav` / `pnavClicks`
- `racterScores`
- `siteAutopilotScore`
- `siteQualityStddev` / `siteQualityStddevs`
- `smallPersonalSite`
- `spambrainLavcScore` / `spambrainLavcScores`
- `url`
- `versionedData`
- `host`

## Critical correction

**siteFocusScore and siteRadius are NOT in this module.** Circulating summaries (including Wikipedia) place them here. Hexdocs v0.4.0 places them in `QualityAuthorityTopicEmbeddingsVersionedItem`. See TOPIC_EMBEDDINGS.md and CORRECTIONS.md.
