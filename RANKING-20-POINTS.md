# 20 Points — Google Ranking Process Reverse Engineered

From verified hexdocs 0.4.0 fields + patents + DOJ testimony. Capacity map, not exact weights.

## Retrieval & Link Graph

1. **Reasonable Surfer per-link weights** (US7716225B1) — `pagerankWeight` in AnchorsAnchor replaces equal PageRank distribution. Formula: `r(A) = α/N + (1-α) × Σ[wᵢ × r(Bᵢ)/|Bᵢ|]`. Features include `fontsize`, `context2` (hash of surrounding terms), `offset`, `locality`/`bucket`.

2. **Source quality tiers** — `sourceType` in AnchorsAnchor: TYPE_HIGH_QUALITY (base docs) < TYPE_MEDIUM_QUALITY (supplemental) < TYPE_LOW_QUALITY (blackhole). Approximate index tier correlation. TYPE_FRESHDOCS treated as HIGH for importance.

3. **Local vs. off-domain anchors** — `isLocal` is a rough same-domain flag. Does not determine onsite/ondomain/offdomain in mustang. `parallelLinks` counts additional links from same source to same target domain (not populated if local).

4. **Anchor spam detection** — IndexingDocjoinerAnchorSpamInfo: `spamProbability`, `spamPenalty`, trusted source matching. IndexingDocjoinerAnchorPhraseSpamInfo: spike detection tagged LINK_SPAM_PHRASE_SPIKE (`phraseAnchorSpamStart/End/Rate/Fraq`).

## Site-Level Quality

5. **siteAuthority in Qstar** — CompressedQualitySignals: "converted from quality_nsr.SiteAuthority, applied in Qstar". Integer. Propagates site-level trust.

6. **NSR (New Site Rank)** — QualityNsrNsrData: `nsr`, `nsrVariance`, `priorAdjustedNsr`, `vlqNsr`, `predictedDefaultNsr` (fallback via Goldmine). Sitechunk-level.

7. **Panda demotions** — CompressedQualitySignals: `pandaDemotion`, `babyPandaDemotion`, `babyPandaV2Demotion`, `exactMatchDomainDemotion`, `navDemotion`, `serpDemotion`, `anchorMismatchDemotion`. Encoding of Panda fields.

8. **Site quality ratio** (US9760641B1 / US9031929, Panda/Lehman) — Reference queries (branded/navigational) / total associated queries. Threshold `T` so new sites start at zero until branded count exceeds threshold.

9. **Chrome data** — `chromeInTotal` in QualityNsrNsrData: site-level Chrome views. Contradicts historical public denials.

10. **Host age sandbox** — `hostAge` in PerDocData: 16-bit day number after 2005-12-31. Used to sandbox fresh spam. `homepagePagerankNs` / `homePageInfo` (trust levels NOT_HOMEPAGE / NOT_TRUSTED / PARTIALLY_TRUSTED / FULLY_TRUSTED) propagate from homepage.

## NavBoost (Click Re-Ranking)

11. **13-month rolling window** — Pandu Nayak (DOJ 2023): NavBoost is one of the most important signals, ~13 months (was 18 pre-2017). Eric Lehman: "not machine learning, just a big table."

12. **Click taxonomy** — QualityNavboostCrapsCrapsClickSignals: `goodClicks`, `badClicks`, `lastLongestClicks` (documented: "last and longest in related user queries"), `impressions`, `unicornClicks`, `unsquashedClicks` / `unsquashedImpressions`.

13. **Slicing** — QualityNavboostCrapsCrapsData: `country`, `language`, `device`, `sliceTag`. `voterTokenCount` (privacy lower bound on distinct users). `unscaledIpPriorBadFraction` (IP prior, craps-penalty.cc). `patternLevel` (0=URL, higher=more general).

14. **Patents** — US8595225B1 (2004, Singhal/Hoelzle): correlating topicality and popularity via user interactions. US8661029B1 / US10229166B1: LC click fraction, IRBoost. NavBoost re-ranks after first-pass scoring.

## Content Quality & Embeddings

15. **OriginalContentScore** — PerDocData: 7-bit, only on thin pages. Real range 0-512. Encode/decode via quality_q2::OriginalContentUtil.

16. **contentEffort** — QualityNsrPQData: `list(QualityNsrVersionedFloatSignal)`. Literal: "LLM-based effort estimation for article pages (see landspeeder/4311817)."

17. **Topic embeddings** — QualityAuthorityTopicEmbeddingsVersionedItem: `siteFocusScore` ("how much a site is focused on one topic"), `siteRadius` ("how far page_embeddings deviate from the site_embedding"), `pageEmbedding`, `siteEmbedding`. QualityNsrNsrData has `site2vecEmbedding` / `site2vecEmbeddingEncoded`.

18. **Information Gain** (US11354342B2, Carbune/Gonnet, 2018/2022) — Scores additional information beyond documents already presented to the user. Session-level in patent text. Aligns with contentEffort / OriginalContentScore direction.

## Freshness & Spam

19. **Freshness** — `lastSignificantUpdate` (PerDocData, UNIX from LSU Selector). `syntacticDate` (CompositeDoc → QualityTimebasedSyntacticDate): `bylineDate`, `trustSyntacticDateInRanking`, `useAsBylineDate`. `hostAge` for sandbox.

20. **Spam systems** — PerDocData: `IsAnchorBayesSpam`, `uacSpamScore` (threshold 64), `keywordStuffingScore`, `GibberishScore`, `spamtokensContentScore` (SiteBoostTwiddler for UGC). SpamBrainData.versionedData at sitechunk. `spambrainLavcScore` in QualityNsrNsrData. AnchorSpamPenalizer (point 4).

## Practical Priorities

- Earn `lastLongestClicks`, avoid `badClicks` (NavBoost, 13-month window).
- Independent links + reference queries → siteAuthority / lower Panda risk.
- High `siteFocusScore`, low `siteRadius`.
- Original effort (`contentEffort`, `OriginalContentScore`).
- Contextual anchors (`pagerankWeight`, `fontsize`, sourceType HIGH).
- Freshness hygiene (accurate byline, real lastSignificantUpdate).
- Spam hygiene (no stuffing, no anchor spikes).

## Limitations

Exact weights unknown. Active vs. deprecated vs. LE-only unknown. Information Gain global vs. session-level unconfirmed. Final IR score formula not in the schema.
