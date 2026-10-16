# Task 02 — Cross-Reference: Leak Fields → Patents → DOJ → Practical Implication

Three-column mapping as defined in Task 01 (task 20: criterion for active ranking factor vs stored feature).

## Criterion (Task 01 #20)

A field counts as an **active ranking factor** if: (a) it appears in a module used in Mustang/TeraGoogle serving (CompressedQualitySignals description says "included in Mustang and TeraGoogle"), AND (b) it has a non-deprecated description indicating application in a scorer (Qstar, Ascorer,Craps), AND (c) it is not marked deprecated/unused. Stored-but-unconfirmed fields are labeled EXPERIMENT or STORED.

## Mapping Table

| Leak Field | Patent | DOJ/Testimony | Status | Practical Implication |
|---|---|---|---|---|
| goodClicks | US11816114B1 (implicit user feedback family) | ABC signals: Clicks. Nayak: ~13mo rolling, sliced by location/device | ACTIVE (CrapsClickSignals in CompressedQualitySignals) | Optimize for sustained engagement; avoid pogo-sticking. Title/description CTR is entry; dwell is the vote. |
| badClicks | US11816114B1 | ABC: Clicks (negative) | ACTIVE | Fast, satisfying pages. Reduce bounce to SERP. |
| lastLongestClicks | US11816114B1 | ABC: Clicks | ACTIVE | Be the last result a user clicks and stays on. Session-level, not just page-level. |
| unicornClicks | (Unicorn = high-trust user segment, internal) | Not directly testified | ACTIVE (subset flag) | High-trust users' behavior weighted. Brand/direct traffic helps. |
| siteAuthority | US9031929B1 (site quality score via branded/nav queries) | Not directly testified; aligns with site quality concepts | ACTIVE (applied in Qstar) | Build brand demand + homepage strength. Site-wide multiplier. |
| siteFocusScore | Topical clustering / entity patents; aligns with US11354342B2 (info gain) conceptually | Not testified | ACTIVE (TopicEmbeddings, superroot) | Deep niche coverage. Off-topic pages penalized via siteRadius. |
| siteRadius | Same cluster | Not testified | ACTIVE | Keep pages aligned to site core topic embedding. |
| OriginalContentScore | US11354342B2 (information gain) | Not testified | ACTIVE (PerDocData) | Original data/experience/analysis. Penalizes rehash. |
| pandaDemotion / babyPandaDemotion / babyPandaV2Demotion | Panda-related patents (site quality) | Panda system confirmed in ranking guide | ACTIVE | Thin/duplicated/low-effort content demoted site-wide. |
| spambrainTotalDocSpamScore / spambrainData | SpamBrain (official system) | SpamBrain in ranking guide | ACTIVE | Avoid keyword stuffing, gibberish, spam patterns. |
| titlematchScore | Phrase-based indexing (Anna Patterson family, US7536408) | Not testified | ACTIVE (NSR) | Title must match query intent precisely. |
| chromeInTotal | Chrome-derived signals | Rand Fishkin highlighted; Google had denied Chrome ranking use | STORED/ACTIVE (site-level Chrome views in NSR) | Popularity measured; direct/brand traffic matters. |
| hostAge | US7346839B2 (historical data) | Not testified | ACTIVE (PerDocData) | Fresh domains sandboxed. |
| experimentalQstar* | Q* experimental framework (go/0DayLEs) | Not testified | EXPERIMENT (not shard-persisted) | Fast live-experiment toggles for new ranking components. |
| ugcDiscussionEffortScore | Quality Rater Guidelines (effort) | Not testified | ACTIVE (CompressedQualitySignals) | UGC effort measured ×1000. |
| productReviewP* | Review quality signals | Not testified | ACTIVE | Review page quality scored for promote/demote. |
| pairwiseqScoringData | — | — | DEPRECATED/unused | Ignore. |
| nsrVersionedData / nsrConfidence / nsrOverrideBid | NSR evolution | Not testified | mixed (nsrOverrideBid: emergency only) | NSR is the site quality backbone. |
| contentEffort | (mentioned in analyses, possibly LLM-era) | Not testified | UNCONFIRMED in hexdocs 0.4.0 | Do not build strategy on it yet. |
| homepagePagerankNs / homePageInfo | PageRank variants + site quality | Not testified | ACTIVE (PerDocData) | New pages inherit homepage authority/trust. |
| site2vecEmbedding | Embeddings / neural matching | Not testified | ACTIVE (NSR + TopicEmbeddings) | Vector alignment helps classic + AI retrieval. |
| voterTokenCount | Privacy-preserving aggregation | Not testified | ACTIVE (CrapsData) | Google filters low-user-count slices for privacy. |
| packedIpAddress / unscaledIpPriorBadFraction | Spam/IP prior (craps-ip-prior.h) | Not testified | ACTIVE | IP-level bad-fraction prior used in Craps penalty. |

## DOJ ABC Framework

- **A = Anchors**: link structures in PerDocData (Anchors*, indexing_docjoiner_anchor_*) + PageRank variants.
- **B = Body**: content fields (OriginalContentScore, bodyWordsToTokensRatio*, titleHardTokenCount*, semanticDate*).
- **C = Clicks**: NavBoost Craps family (goodClicks, badClicks, lastLongestClicks, unicornClicks, impressions).

Patent + leak + testimony converge: the three pillars are links, content, and user behavior, with site-level quality as multiplier.