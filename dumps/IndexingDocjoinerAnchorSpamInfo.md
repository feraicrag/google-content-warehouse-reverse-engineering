# IndexingDocjoinerAnchorSpamInfo

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.IndexingDocjoinerAnchorSpamInfo.html

Header: Summarizes output of AnchorSpamPenalizer. Spammy anchors tagged LINK_SPAM_PHRASE_PENALIZER and demoted to SPAM locality in anchor-localizer.cc.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| anchorEnd | integer() | nil | End date of last anchor. |
| anchorFraq | number() | nil | Ratio of spam demoted period to all anchor period. |
| anchorStart | integer() | nil | Start date of first anchor. |
| demoted | integer() | nil | How many anchors were demoted. |
| demotedAll | boolean() | nil | Demoted all or only spam-classified. |
| demotedEnd | integer() | nil | End date of demotion period. |
| demotedStart | integer() | nil | Start date of demotion period. |
| phraseCount | number() | nil | Spam phrases found among unique domains. |
| phraseDays | number() | nil | Days over which 80% of phrases discovered. |
| phraseFraq | number() | nil | Spam phrases fraction of all anchors. |
| phraseRate | number() | nil | Average daily rate of spam anchor discovery. |
| processed | integer() | nil | Total processed anchors. |
| sampled | boolean() | nil | True if anchors sampled during observation. |
| sources | list(IndexingDocjoinerAnchorTrustedInfo) | nil | Trusted sources. Only when --anchorspam_penalizer_debug=true. |
| spamDebugInfo | String.t | nil | Debug info for spam probability. |
| spamPenalty | number() | nil | Combined penalty for anchor demotion. |
| spamProbability | number() | nil | Predicted probability of spam. |
| trustedDemoted | integer() | nil | Trusted anchors used in spam probability. |
| trustedExamples | String.t | nil | Examples of trusted sources. |
| trustedMatching | integer() | nil | Trusted anchors with text matching spam terms. |
| trustedTarget | boolean() | nil | True if URL is on trusted source. |
| trustedTotal | integer() | nil | Total trusted sources for this URL. |
