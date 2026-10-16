# PerDocData — complete field extraction (hexdocs v0.4.0)

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.PerDocData.html

70+ fields. Listed verbatim with types and descriptions where present.

## Spam & quality scores

- `DocLevelSpamScore` (integer) — document spam score, 7-bit 0–127
- `GibberishScore` (integer)
- `KeywordStuffingScore` (integer)
- `SpamWordScore` (integer)
- `IsAnchorBayesSpam` (integer)
- `ScaledSpamScoreEric` (integer) — 7-bit 0–127
- `ScaledSpamScoreYoram` (integer) — 7-bit 0–127
- `ScaledExptSpamScoreEric` (integer)
- `ScaledExptSpamScoreYoram` (integer)
- `ScaledExptIndyRank1/2/3` (integer) — experimental
- `ScaledLinkAgeSpamScore` (integer)
- `spamrank` (integer)
- `spambrainTotalDocSpamScore` (integer)
- `spambrainData` → SpamBrainData (host-v1 sitechunk scores)
- `spambrainDomainSitechunkData`
- `spamMuppetSignals` → SpamMuppetjoinsMuppetSignals (hacked-site signals; as of Oct'19 stored in separate corpus)
- `spamtokensContentScore` (number) — SpamTokens content scores; used in SiteBoostTwiddler for UGC spam; see go/spamtokens-dd
- `spamCookbookAction`
- `uacSpamScore` (integer) — 7-bit 0–127; threshold 64; >=64 = uac spam
- `trendspamScore` (integer) — count of matching trendspam queries
- `urlPoisoningData` → UrlPoisoningData (suppress spam documents)

## Authority & links

- `pagerank` (number)
- `pagerank2` (number)
- `pagerank0/1/2` variants
- `crawlPagerank`
- `toolbarPagerank`
- `homepagePagerankNs` (integer) — page-rank of the site's homepage, copied from cdoc.doc().pagerank_ns() of the homepage
- `homePageInfo` — homepage trust levels (NOT_HOMEPAGE / NOT_TRUSTED / PARTIALLY_TRUSTED / FULLY_TRUSTED)
- `ScaledIndyRank` (integer)
- `ScaledExptIndyRank` (integer)
- `nsrDataProto` → QualityNsrNsrData (stripped site-level signals)
- `topPetacatTaxId` (integer) — top petacat of the site; used in SiteboostTwiddler
- `smearingMaxTotalOffdomainAnchors` (integer)

## Freshness & dates

- `domainAge`
- `hostAge`
- `lastSignificantUpdate` (string) — UNIX timestamp seconds; sourced from quality_timebased.LastSignificantUpdate via LSUSelector
- `lastSignificantUpdateInfo`
- `semanticDate` / `semanticDateConfidence` (deprecated → semanticDateInfo) / `semanticDateInfo`
- `timeSensitivity`
- `freshnessEncodedSignals`
- `freshboxArticleScores`
- `datesInfo` (string) — dates-related info; used in FreshnessTwiddler; encode/decode via quality/timebased/utils/dates-info-helper-inl.h
- `eventsDate`

## Content

- `OriginalContentScore` (integer) — 7-bit 0–127; only pages with little content have this field; actual range 0–512; encode/decode via quality_q2::OriginalContentUtil
- `bodyWordsToTokensRatioBegin` (number)
- `bodyWordsToTokensRatioTotal` (number)
- `originalTitleHardTokenCount` (integer)
- `titleHardTokenCountWithoutStopwords` (integer)
- `commercialScore` (integer)
- `TagPageScore`
- `scienceDoctype` (integer) — <0 not science; 0 fully visible; >0 limited visibility (visible terms count)
- `inNewsstand`
- `isHotdoc`
- `numUrls` (integer) — total URLs encoded = alternate URLs + 1
- `onsiteProminence`
- `WhirlpoolDiscount`
- `ymylHealthScore` (integer) — YMYL health classifier scores (go/ymyl-classifier-dd); requires joining g/pq-classifiers-announce

## Authorship & entities

- `authorObfuscatedGaiaStr` (list<string>)
- `mediaOrPeopleEntities` → ImageQualitySensitiveMediaOrPeopleEntities (5 most topical KG entities)
- `webrefEntities` → RepositoryWebrefWebrefMustangAttachment (go/webref)
- `languages` / `rosettaLanguages` / `saftLanguageInt`
- `countryInfo` / `geodata` / `brainloc`

## Submodule pointers

- `compressedQualitySignals` → CompressedQualitySignals
- `biasingdata` / `biasingdata2`
- `crowdingdata` / `imagedata` / `mobileData` / `smartphoneData`
- `oceandata` / `phildata` / `kaltixdata` / `groupsData` / `BlogData` / `BookCitationData`
- `PremiumData` / `ToolBarData` / `fireflySiteSignal`
- `pageTags` (list<integer>)
- `localizedCluster` / `servingTimeClusterIds`
- `shingleInfo` / `queriesForWhichOfficial` / `productSitesInfo` / `launchAppInfo`
- `rsApplication` / `s3AudioLanguage`
- `desktopInterstitials` / `noimageframeoverlayreason`
- `socialgraphNodeNameFp` / `knexAnnotation` (FreshDocs k'nex annotations)
- `liveResultsData` / `contentAttributions` / `extraData` / `crawlerIdProto`
- `pageregions`
- `videoLanguage` → QualityVidyaVideoLanguageVideoLanguage (audio-based LID, watch pages only)
- `fringeQueryPrior` → QualityFringeFringeQueryPriorPerDocData (contact fringe-ranking team; do not use directly)
- `tundraClusterId` (integer) — deprecated; use equivalent inside nsr_data_proto
- `webmirrorEcnFp` (string)
- `scaledSelectionTierRank` (integer) — 0–32767, language-normalized over serving tier
- `Event` (list<PerDocDebugEvent>) — free-form debug info

## Deprecated

- `AUTHORObfuscatedGaia` (use string version)
- `QuarantineWhitelist` (boolean)

## Cross-check notes

- `homepagePagerankNs` and `homePageInfo` confirmed HERE in PerDocData (not in CompressedQualitySignals).
- Full verbatim scrape of the hexdocs HTML page was partial in this pass; remaining fields should be re-scraped in Task 2 for 100% coverage.
