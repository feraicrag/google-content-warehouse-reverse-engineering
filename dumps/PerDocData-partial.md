# PerDocData (partial — Next tag 225)

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.PerDocData.html

Header: Used in both indexing and serving. In mustang serving, only decoded during search phase. Should only contain data used during search. Next tag: 225

Key fields extracted (full list in hexdocs):

| Field | Type | Description |
|-------|------|-------------|
| OriginalContentScore | integer() | 7-bit (0-127). Only on thin pages. Real range 0-512. Encode/decode via quality_q2::OriginalContentUtil. |
| homepagePagerankNs | integer() | Page-rank of homepage. Copied from cdoc.doc().pagerank_ns(). |
| homePageInfo | integer() | Trust level enum. |
| hostAge | integer() | 16-bit day number after 2005-12-31. Sandbox fresh spam. |
| lastSignificantUpdate | String.t | UNIX timestamp from LSUSelector. |
| lastSignificantUpdateInfo | String.t | Metadata. Use helpers from lsu-helper.h. |
| semanticDate | integer() | 32-bit UNIX. Estimated from content, anchors, related docs. |
| semanticDateInfo | integer() | Confidence for day/month/year components. |
| onsiteProminence | integer() | 13-bit. Importance within site. Propagated from homepage and high craps click pages. |
| uacSpamScore | integer() | 7-bit. Threshold 64. |
| IsAnchorBayesSpam | boolean() | Anchor bayes classifier. |
| DocLevelSpamScore | integer() | 7-bit. |
| KeywordStuffingScore | integer() | — |
| GibberishScore | integer() | — |
| SpamWordScore | integer() | 7-bit. |
| spamtokensContentScore | number() | Used in SiteBoostTwiddler for UGC spam. go/spamtokens-dd |
| spambrainData | SpamBrainData | Host-v1 sitechunk level. |
| spambrainDomainSitechunkData | SpamBrainData | Domain sitechunk level. |
| nsrDataProto | QualityNsrNsrData | Stripped site-level signals. |
| compressedQualitySignals | CompressedQualitySignals | — |
| webrefEntities | RepositoryWebrefWebrefMustangAttachment | Deprecated → UDR. |
| queriesForWhichOfficial | OfficialPagesQuerySet | (query, country, language) triples where this is official page. |
| scaledSelectionTierRank | integer() | 0-32767. Language normalized over serving tier. |
| commercialScore | number() | >0 indicates commercial. |
| ymylHealthScore / ymylNewsScore | integer() | Require pq-classifiers-announce join. |
| isHotdoc | boolean() | Set by FreshDocs instant doc joiner. |
| hostNsr | integer() | Deprecated. Use nsr_data_proto. |
| nsrIsCovidLocalAuthority / nsrIsElectionAuthority / nsrIsVideoFocusedSite | boolean() | Deprecated. Use nsr_data_proto. |

Full attribute list continues in hexdocs. See source for complete set (Next tag 225).
