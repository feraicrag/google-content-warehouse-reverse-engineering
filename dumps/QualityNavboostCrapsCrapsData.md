# QualityNavboostCrapsCrapsData

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityNavboostCrapsCrapsData.html

Header: NEXT TAG: 28

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| badClicks | float() | nil | — |
| clicks | float() | nil | — |
| country | String.t | nil | Two-letter uppercase country slice. Examples: US, FR, BR. |
| device | QualityNavboostCrapsCrapsDevice | nil | Device interface and os slice. |
| features | list(QualityNavboostCrapsFeatureCrapsData) | nil | CrapsClickSignals for specific features (mobile, US, metro id). |
| goodClicks | float() | nil | — |
| impressions | float() | nil | May become legacy; may retire in favor of squashed field. |
| language | String.t | nil | Language slice. Examples: en, fr, pt-BR. |
| lastLongestClicks | float() | nil | The number of clicks that were last and longest in related user queries. |
| mobileData | QualityNavboostCrapsCrapsData | nil | DO NOT USE. Use mobileSignals. Present in legacy protos. |
| mobileSignals | QualityNavboostCrapsCrapsClickSignals | nil | Portion aggregated on data from tier 1/2 mobile interfaces in QSessions. |
| packedIpAddress | String.t | nil | Packed string in network byte order for CrapsIpPrior. |
| patternLevel | integer() | nil | Level of pattern. 0=URL. Higher=more general. |
| patternSccStats | QualityNavboostCrapsStatsWithWeightsProto | nil | For pattern data, stats of SCCs of contributing URLs. |
| query | String.t | nil | — |
| sliceTag | String.t | nil | Arbitrary string for slicing by device, country, locale. Aggregated separately. |
| squashed | QualityNavboostCrapsCrapsClickSignals | nil | Not used yet. |
| unscaledIpPriorBadFraction | float() | nil | Prior based on IP address. Prior to linear transform in craps-penalty.cc. |
| unsquashed | QualityNavboostCrapsCrapsClickSignals | nil | For retuning rollout. |
| unsquashedMobileSignals | QualityNavboostCrapsCrapsClickSignals | nil | — |
| url | String.t | nil | — |
| voterTokenCount | integer() | nil | Lower bound on distinct users. Used for privacy-related filtering. |
