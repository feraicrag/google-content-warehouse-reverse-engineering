# CompressedQualitySignals — complete field extraction (hexdocs v0.4.0)

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.CompressedQualitySignals.html

Module description (verbatim): "A message containing per doc signals that are compressed and included in Mustang and TeraGoogle." Next id: 42.

## Fields

- `siteAuthority` (integer) — **VERIFIED**. Literal description: "converted from quality_nsr.SiteAuthority, applied in Qstar". This is the site-wide authority score circulating analyses cite.
- `babyPandaDemotion`
- `babyPandaV2Demotion`
- `pandaDemotion`
- `exactMatchDomainDemotion`
- `authorityPromotion`
- `unauthoritativeScore`
- `scamness`
- `crapsAbsoluteHostSignals`
- `crapsNewHostSignals`
- `crapsNewPatternSignals`
- `crapsNewUrlSignals`
- `crapsUnscaledIpPriorBadFraction`
- `navDemotion`
- `pqData`
- `serpDemotion`
- `anchorMismatchDemotion`
- `ugcDiscussionEffortScore`
- `productReviewPPromotePage` / `productReviewPDemotePage` / `productReviewPPromoteSite` / `productReviewPDemoteSite`
- `topicEmbeddingsVersionedData`
- `experimentalQstarDeltaSignal`
- `experimentalNsrTeamData`
- `vlqNsr`

## Notes

- siteAuthority sits alongside Panda demotions and Q* experimental signals — same compressed bundle shipped to Mustang/TeraGoogle.
- `topicEmbeddingsVersionedData` is the pointer toward siteFocusScore/siteRadius (see TOPIC_EMBEDDINGS.md).
- homepagePagerankNs / homePageInfo are NOT in this module (they are in PerDocData).
