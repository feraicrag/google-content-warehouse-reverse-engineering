# NavBoost / Craps — complete field extraction (hexdocs v0.4.0)

## QualityNavboostCrapsCrapsData (22 fields)

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityNavboostCrapsCrapsData.html

- `query` (string)
- `url` (string)
- `country` (string) — two-letter uppercase slice ("US", "FR", "BR")
- `language` (string) — slice ("en", "fr", "pt-BR")
- `device` → QualityNavboostCrapsCrapsDevice
- `sliceTag` (string) — arbitrary string for slicing by device/country/locale; aggregated separately per tag
- `patternLevel` (integer) — more general patterns get higher values; URL pattern = 0
- `patternSccStats` → QualityNavboostCrapsStatsWithWeightsProto
- `goodClicks` (float)
- `badClicks` (float)
- `clicks` (float)
- `impressions` (float) — "may become legacy; may retire and use squashed instead"
- `lastLongestClicks` (float) — "number of clicks that were last and longest in related user queries"
- `squashed` → CrapsClickSignals — "not used yet"
- `unsquashed` → CrapsClickSignals — "we will start using this one for the retuning rollout"
- `mobileData` → CrapsData — **DO NOT USE** (legacy; use mobileSignals); do not remove (golden tests)
- `mobileSignals` → CrapsClickSignals — tier 1/2 mobile interfaces in QSessions
- `unsquashedMobileSignals` → CrapsClickSignals
- `features` (list<FeatureCrapsData>) — CrapsClickSignals for specific features
- `voterTokenCount` (integer) — lower bound on distinct users; privacy filtering
- `packedIpAddress` (string) — network byte order; only if ip_prior looked up at retrieval
- `unscaledIpPriorBadFraction` (float) — prior based on IP; see craps-ip-prior.h; pre-transformation value from craps-penalty.cc

## QualityNavboostCrapsCrapsClickSignals (10 fields)

- `goodClicks`
- `badClicks`
- `clicks`
- `impressions`
- `lastLongestClicks`
- `unicornClicks`
- `absoluteImpressions` — **comment: "only used at host level for unsquashed impressions"**
- `unsquashedClicks`
- `unsquashedImpressions`
- `unsquashedLastLongestClicks`

## DOJ alignment

Pandu Nayak testimony: NavBoost = ~13-month rolling aggregated click data, sliced by location/device. ABC framework: Anchors, Body, Clicks. The CrapsClickSignals taxonomy matches the "good/bad/last-longest" framing from trial materials.
