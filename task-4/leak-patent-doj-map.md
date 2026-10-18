# Leak — Patent — DOJ Cross-Map

Primary sources: hexdocs 0.4.0 modules (verified), patents (USPTO), DOJ trial exhibits (US v. Google).

## 1. NavBoost / Click Signals

| Leak Field | Module | Patent | DOJ Evidence | Notes |
|------------|--------|--------|--------------|-------|
| goodClicks | QualityNavboostCrapsCrapsClickSignals / CrapsData | US10229166B1 "Modifying search result ranking based on implicit user feedback" | Pandu Nayak testimony: NavBoost is one of the most important signals; ~13-month rolling window | Long clicks / engaged clicks |
| badClicks | same | same | same | Short clicks / bounce-back |
| lastLongestClicks | same | same | same | Documented: "The number of clicks that were last and longest in related user queries" |
| impressions | same | US8595225B1 (2004, Singhal/Hoelzle) | same | Base for CTR |
| unicornClicks | same | — | — | Subset from Unicorn users |
| unsquashedClicks / unsquashedImpressions | same | — | — | Pre-normalization |
| country / language / device / sliceTag | QualityNavboostCrapsCrapsData | — | — | Sliced aggregation |
| voterTokenCount | same | — | — | Privacy lower bound on distinct users |
| unscaledIpPriorBadFraction | same | — | — | IP prior before transform (craps-penalty.cc) |

Architecture: CompositeDoc → PerDocData → compressedQualitySignals / nsrDataProto. NavBoost re-ranks after first-pass scoring.

## 2. Reasonable Surfer / Anchor Weighting

| Leak Field | Module | Patent | Notes |
|------------|--------|--------|-------|
| pagerankWeight | AnchorsAnchor | US7716225B1 "Ranking documents based on user behavior and/or feature data" (Dean/Anderson/Battle, 2004) | Per-link weight for pageranker |
| fontsize | AnchorsAnchor | same | Feature for click probability |
| context2 | AnchorsAnchor | same | Hash of surrounding terms |
| locality / bucket | AnchorsAnchor | same | Quality measure |
| sourceType | AnchorsAnchor | — | HIGH/MEDIUM/LOW_QUALITY correlated with index tier |
| isLocal | AnchorsAnchor | — | Rough same-domain indicator |

Formula from patent: r(A) = α/N + (1-α) × Σ[wᵢ × r(Bᵢ)/|Bᵢ|]. Weights learned from positive/negative click instances.

## 3. Site Quality / NSR / Panda

| Leak Field | Module | Patent | Notes |
|------------|--------|--------|-------|
| siteAuthority | CompressedQualitySignals | US9760641B1 / US9031929 (Panda/Lehman, "Site quality score") | "converted from quality_nsr.SiteAuthority, applied in Qstar" |
| nsr | QualityNsrNsrData | same family | Site-level quality score |
| predictedDefaultNsr | QualityNsrPQData | — | Fallback when no direct NSR |
| pandaDemotion | CompressedQualitySignals | Site quality patents | Encoding of Panda fields |
| babyPandaDemotion / babyPandaV2Demotion | same | — | Additional demotions |
| chromeInTotal | QualityNsrNsrData | — | Site-level Chrome views (contradicts public denials) |
| hostAge | PerDocData | — | 16-bit day number after 2005-12-31; used to sandbox fresh spam |
| homepagePagerankNs | PerDocData | — | PageRank of homepage copied from cdoc |

Panda modifier from related analysis: M = IL / RQ (independent links / reference queries).

## 4. Originality / Effort / Information Gain

| Leak Field | Module | Patent | Notes |
|------------|--------|--------|-------|
| OriginalContentScore | PerDocData | US11354342B2 "Contextual Estimation of Link Information Gain" (Carbune/Gonnet, 2018/2022) | 7-bit, only on thin pages; real range 0-512 |
| contentEffort | QualityNsrPQData | same direction | "LLM-based effort estimation for article pages (landspeeder/4311817)" |
| siteFocusScore | QualityAuthorityTopicEmbeddingsVersionedItem | — | How focused a site is on one topic |
| siteRadius | same | — | Deviation of page embeddings from site embedding |
| site2vecEmbedding / site2vecEmbeddingEncoded | QualityNsrNsrData | — | Site-level embeddings |

Information Gain patent scores additional information beyond documents already presented to the user (session-level, not necessarily global).

## 5. ABC Signals (DOJ Exhibit)

From DOJ trial documents (hand-crafted signals):

- **A** — Anchors (source → target links)
- **B** — Body (terms in document)
- **C** — Clicks (historically, how long a user stayed before bouncing)

Most signals except RankBrain and DeepRank are hand-crafted; engineers fit curves on data + rater labels.

## 6. Spam / Demotion Systems

| Leak Field | Module | Notes |
|------------|--------|-------|
| spamProbability | IndexingDocjoinerAnchorSpamInfo | Predicted probability from AnchorSpamPenalizer |
| spamPenalty | same | Combined demotion |
| phraseAnchorSpam* | IndexingDocjoinerAnchorPhraseSpamInfo | Spike detection; tagged LINK_SPAM_PHRASE_SPIKE |
| spambrainLavcScore | QualityNsrNsrData | July 2022 LAVC (go/cloverfield-lavc-deck) |
| versionedData | SpamBrainData | Versioned SB classifiers at sitechunk level |
| IsAnchorBayesSpam | PerDocData | Boolean |
| uacSpamScore | PerDocData | 7-bit, threshold 64 |
| keywordStuffingScore / GibberishScore | PerDocData | 7-bit each |

## 7. Freshness / Dates

| Leak Field | Module | Notes |
|------------|--------|-------|
| lastSignificantUpdate | PerDocData | UNIX timestamp from LSU Selector |
| semanticDate | PerDocData | 32-bit UNIX; confidence encoded |
| syntacticDate | CompositeDoc → QualityTimebasedSyntacticDate | bylineDate, trustSyntacticDateInRanking, useAsBylineDate |
| freshnessEncodedSignals | PerDocData | Deprecated |
| hostAge | PerDocData | Sandbox fresh spam |

## Architecture Summary

```
CompositeDoc (Next id: 194)
├── perDocData → PerDocData (Next tag: 225)
│   ├── compressedQualitySignals → CompressedQualitySignals (Next id: 43)
│   │   ├── siteAuthority, pandaDemotion, babyPanda*, scamness, topicEmbeddingsVersionedData
│   │   └── experimentalQstar* (serving-time LE only)
│   ├── nsrDataProto → QualityNsrNsrData (Next ID: 63)
│   │   ├── nsr, site2vecEmbedding, chardEncoded, chromeInTotal, spambrainLavcScore
│   │   └── isVideoFocusedSite, isElectionAuthority, clusterId
│   ├── webrefEntities → RepositoryWebrefWebrefMustangAttachment (DEPRECATED → UDR)
│   ├── spambrainData → SpamBrainData
│   └── OriginalContentScore, hostAge, homepagePagerankNs, lastSignificantUpdate
├── anchors → Anchors → AnchorsAnchor (pagerankWeight, sourceType, locality)
├── properties → DocProperties
└── syntacticDate → QualityTimebasedSyntacticDate
```

NavBoost (Craps) re-ranks on top using sliced click aggregates.
