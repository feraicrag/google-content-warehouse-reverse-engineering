# CompressedQualitySignals

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.CompressedQualitySignals.html

Header: A message containing per-doc signals that are compressed and included in Mustang and TeraGoogle. For TeraGoogle, this message is included in perdocdata which means it can be used in preliminary scoring. CAREFUL: For TeraGoogle, this data resides in very limited serving memory (Flash storage) for a huge number of documents. Next id: 43

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| ugcDiscussionEffortScore | integer() | nil | UGC page quality signals. (Times 1000 and floored) |
| productReviewPPromotePage | integer() | nil | — |
| experimentalQstarDeltaSignal | number() | nil | Not propagated to shards. Populated at serving time for experimental Q* LEs. See go/0DayLEs. |
| productReviewPDemoteSite | integer() | nil | Product review demotion/promotion confidences. (Times 1000 and floored) |
| experimentalQstarSiteSignal | number() | nil | Not propagated to shards. Populated at serving time for experimental Q* LEs. |
| exactMatchDomainDemotion | integer() | nil | Converted from QualityBoost.emd.boost. Float [0,1] to int [0,1023] (10 bits). |
| nsrVersionedData | list(NSRVersionedItem) | nil | Deprecated. Use nsr_data_proto. |
| nsrConfidence | integer() | nil | Deprecated. Use nsr_variance in nsr_data_proto. |
| lowQuality | integer() | nil | S2V low quality score. Converted from quality_nsr.NsrData, applied in Qstar. |
| navDemotion | integer() | nil | Converted from QualityBoost.nav_demoted.boost. |
| pqData | integer() | nil | Encoded page-level PQ signals. |
| siteAuthority | integer() | nil | Converted from quality_nsr.SiteAuthority, applied in Qstar. |
| crapsNewUrlSignals | String.t | nil | Use quality/navboost/craps/craps-lossy-compression.h. Do not access directly. |
| babyPandaV2Demotion | integer() | nil | New BabyPanda demotion, applied on top of Panda. Meant to replace babyPandaDemotion. |
| authorityPromotion | integer() | nil | Converted from QualityBoost.authority.boost. |
| productReviewPUhqPage | integer() | nil | Possibility of page being a high quality review page. |
| crapsAbsoluteHostSignals | integer() | nil | Impressions, unsquashed, host level. Not to be used with compressed ratios. |
| productReviewPPromoteSite | integer() | nil | — |
| nsrOverrideBid | number() | nil | Deprecated. Use nsr_data_proto. |
| babyPandaDemotion | integer() | nil | Converted from QualityBoost.rendered.boost. |
| serpDemotion | integer() | nil | Applied in Qstar. |
| anchorMismatchDemotion | integer() | nil | Converted from QualityBoost.mismatched.boost. |
| crapsNewHostSignals | String.t | nil | — |
| experimentalQstarSignal | number() | nil | Not propagated to shards. Populated at serving time for experimental Q* LEs. |
| pairwiseqScoringData | PairwiseQScoringData | nil | Deprecated and unused. |
| topicEmbeddingsVersionedData | list(QualityAuthorityTopicEmbeddingsVersionedItem) | nil | Versioned TopicEmbeddings data for superroot / scorers. |
| scamness | integer() | nil | Scam model score. Qstar signal. Range 0-1023. |
| crapsUnscaledIpPriorBadFraction | integer() | nil | — |
| pandaDemotion | integer() | nil | Encoding of Panda fields in SiteQualityFeatures. Encoding via quality_coati::coati_util. |
| unauthoritativeScore | integer() | nil | Unauthoritative score. Qstar signal. |
| experimentalNsrTeamWsjData | list(QualityNsrExperimentalNsrTeamWSJData) | nil | Not propagated to shards. Populated at serving time by go/web-signal-joins. LE only. |
| experimentalNsrTeamData | QualityNsrExperimentalNsrTeamData | nil | Not propagated to shards. Populated at serving time. LE only. |
| productReviewPReviewPage | integer() | nil | Possibility of page being a review page. See go/pr-boosts. |
| pqDataProto | QualityNsrPQData | nil | Stripped page-level signals, not present in encoded pq_data. |
| pairwiseqVersionedData | list(PairwiseQVersionedItem) | nil | Versioned PairwiseQ score. |
| crapsNewPatternSignals | String.t | nil | — |
| vlqNsr | integer() | nil | Deprecated. Use nsr_data_proto. |
| productReviewPDemotePage | integer() | nil | — |
