# QualityTimebasedSyntacticDate

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityTimebasedSyntacticDate.html

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| bylineDate | String.t | nil | Set only when byline differs from date. Within 24h of crawl or timezone difference. |
| date | String.t | nil | Seconds since epoch. Can be negative (pre-1970). |
| daterange | QualityTimebasedSyntacticDateDateRange | nil | — |
| debugInfo | String.t | nil | — |
| fromExplicitTimeZone | boolean() | nil | Source has explicit timezone. Internal only. |
| info | integer() | nil | Bit 1 = high confidence byline. Bit 2 = high confidence byline without content age. |
| position | QualityTimebasedSyntacticDatePosition | nil | — |
| precisionMark | integer() | nil | PRECISION_MARK type. |
| syntacticDateNotForRestrict | boolean() | nil | Do not use in date restricts. |
| timeZoneOffsetSeconds | String.t | nil | Timezone offset in seconds. Internal only. |
| trustSyntacticDateInRanking | boolean() | nil | High confidence but not byline. |
| useAsBylineDate | boolean() | nil | Good for snippet byline display. |
| useInTimeZoneGuessingMode | boolean() | nil | Good for site-level timezone guessing. |
| useRangeInsteadOfDateForRestrict | boolean() | nil | Use DateRange as restrict if true. |
