# QualityNsrNsrData

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityNsrNsrData.html

Header: NOTE: When adding a new field to be propagated to Raffia check if NsrPatternSignalSpec needs to be updated. Next ID: 63

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| ugcScore | number() | nil | — |
| spambrainLavcScores | list(QualityNsrVersionedFloatSignal) | nil | — |
| titlematchScore | number() | nil | Titlematch score of the site. How well titles match user queries. |
| site2vecEmbeddingEncoded | list(QualityNsrNsrDataEncodedEmbedding) | nil | Encoded site2vec embedding for superroot. |
| smallPersonalSite | number() | nil | Score of small personal site promotion. go/promoting-personal-blogs-v1 |
| pnavClicks | number() | nil | Denominator for pnav computation. |
| siteChunkSource | String.t | nil | Only annotated in Goldmine NSR annotator. |
| clusterUplift | QualityNsrNsrDataClusterUplift | nil | — |
| siteAutopilotScore | number() | nil | Aggregated url autopilot scores for this sitechunk. |
| isVideoFocusedSite | boolean() | nil | >50% watch pages (with smoothing). Not on known video-hosting domains. |
| metadata | QualityNsrNsrDataMetadata | nil | — |
| chromeInTotal | number() | nil | Site-level Chrome views. |
| chardVariance | number() | nil | — |
| chardScoreVariance | list(QualityNsrVersionedFloatSignal) | nil | Site-level Chard Variance. |
| chardScoreEncoded | list(QualityNsrVersionedIntSignal) | nil | Site-level Chard (encoded as int). |
| nsrdataFromFallbackPatternKey | boolean() | nil | True if NSR data is average of other host chunks. |
| siteQualityStddevs | list(QualityNsrVersionedFloatSignal) | nil | — |
| clusterId | integer() | nil | Cluster id for ecosystem experiments (Tundra). |
| videoScore | number() | nil | — |
| shoppingScore | number() | nil | — |
| nsr | number() | nil | — |
| localityScore | number() | nil | Locality component of LocalAuthority signal. go/pq-localauthority |
| siteChunk | String.t | nil | Primary NSR sitechunk. Usually HOST_LEVEL_V3. Rare cases based on page markup. |
| i18nBucket | integer() | nil | Corresponds to i18n_g42_bucket. |
| chardEncoded | integer() | nil | Site-level chard score. Site quality predictor based on content. |
| articleScoreV2 | number() | nil | — |
| nsrEpoch | String.t | nil | Epoch from which this NSR value comes. |
| tofu | number() | nil | Site-level tofu score. Site quality predictor based on content. |
| siteLinkOut | number() | nil | Aggregated url link out scores for this sitechunk. |
| nsrOverrideBid | number() | nil | Emergency override of NSR as bid in Q*. >0.001 to take effect. go/nsr-override-bid |
| language | integer() | nil | — |
| clutterScores | list(QualityNsrVersionedFloatSignal) | nil | — |
| host | String.t | nil | — |
| isCovidLocalAuthority | boolean() | nil | Local authority covid signal. go/covid-local-authority |
| pnav | number() | nil | Fractional signals. |
| siteQualityStddev | number() | nil | Estimate of site PQ rating stddev. Different from nsr_variance. |
| impressions | number() | nil | Site-level impressions. |
| directFrac | number() | nil | — |
| vlq | number() | nil | Score of the Video LQ model. |
| racterScores | list(QualityNsrVersionedFloatSignal) | nil | Site-level AGC classification score. go/project-racter-overview |
| spambrainLavcScore | number() | nil | SpamBrain LAVC score as of July 2022. go/cloverfield-lavc-deck |
| url | String.t | nil | — |
| secondarySiteChunk | String.t | nil | Secondary NSR sitechunk. More granular than primary. |
| articleScore | number() | nil | Score from article classification of the site. |
| site2vecEmbedding | list(QualityNsrNsrDataEmbedding) | nil | Site2vec embeddings. |
| versionedData | list(QualityNsrNSRVersionedData) | nil | Versioned map of NSR values for next release experiments. |
| siteLinkIn | number() | nil | Average site_link_in for pages in sitechunk. |
| ketoVersionedData | list(QualityNsrKetoKetoVersionedData) | nil | Keto data. |
| ymylNewsV2Score | number() | nil | — |
| isElectionAuthority | boolean() | nil | Election authority signal. go/election-authority |
| sitePr | number() | nil | — |
| priorAdjustedNsr | list(QualityNsrVersionedFloatSignal) | nil | NSR - prior. Estimate of whether site is above/below average in its slice. |
| healthScore | number() | nil | Categorical signals. |
| clutterScore | number() | nil | Delta site-level signal penalizing distracting resources. go/clutter-v0 |
| vlqNsr | number() | nil | NSR from headroom model targeting low-quality video sites. |
| nsrVariance | number() | nil | — |
