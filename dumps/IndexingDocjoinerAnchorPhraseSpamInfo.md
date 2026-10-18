# IndexingDocjoinerAnchorPhraseSpamInfo

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.IndexingDocjoinerAnchorPhraseSpamInfo.html

Header: Signals identify spike of spammy anchor phrases. Anchors created during spike tagged LINK_SPAM_PHRASE_SPIKE.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| phraseAnchorSpamCount | number() | nil | Spam phrases found among unique domains. |
| phraseAnchorSpamDays | number() | nil | Days over which 80% discovered. |
| phraseAnchorSpamDemoted | integer() | nil | Total demoted anchors. |
| phraseAnchorSpamEnd | integer() | nil | Time when spike ended with padding. |
| phraseAnchorSpamFraq | number() | nil | Spam phrases fraction of all anchors. |
| phraseAnchorSpamPenalty | number() | nil | Combined penalty. |
| phraseAnchorSpamProcessed | integer() | nil | Total observed anchors. |
| phraseAnchorSpamRate | number() | nil | Average daily rate. |
| phraseAnchorSpamStart | integer() | nil | Time when spike started with padding. |
