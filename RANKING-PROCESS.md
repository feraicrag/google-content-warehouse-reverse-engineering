# Google Ranking Process — Reverse Engineered

Synthesized from: hexdocs 0.4.0 verified fields, USPTO patents, DOJ trial testimony (Pandu Nayak, 2023).

This is a capacity map, not a claim of exact weights or current production mix. Many fields may be deprecated, LE-only, or inactive.

## Architecture Overview

```
Query
  ↓
Retrieval (anchors + body + embeddings)
  ↓
First-pass scoring (ABC + site quality)
  ↓
NavBoost re-rank (13-month click aggregates, sliced)
  ↓
Twiddlers / post-processing
  ↓
SERP
```

CompositeDoc is the root container. PerDocData holds most document signals. CompressedQualitySignals and QualityNsrNsrData hold site-level quality. Anchors/AnchorsAnchor hold the link graph with per-link weights.

## Layer 1: Retrieval

**Anchors (A)** — Reasonable Surfer model (US7716225B1, Dean/Anderson/Battle, 2004).

Original PageRank treated links equally. Reasonable Surfer replaces that with per-link weight `wᵢ` based on predicted click probability:

```
r(A) = α/N + (1-α) × Σ[wᵢ × r(Bᵢ)/|Bᵢ|]
```

Leak fields in AnchorsAnchor:
- `pagerankWeight` — weight stored for pageranker
- `fontsize` — feature for click probability
- `locality` / `bucket` — quality measure (see quality/anchors/definitions.h)
- `context2` — hash of surrounding terms
- `sourceType` — HIGH < MEDIUM < LOW quality of source page (approximate index tier)
- `isLocal` — rough same-domain flag (does not determine onsite/offdomain in mustang)
- `firstseenDate` — days past 1994-12-31

**Body (B)** — term matching + embeddings.
- `site2vecEmbedding` / `site2vecEmbeddingEncoded` (QualityNsrNsrData)
- `pageEmbedding` / `siteEmbedding` (QualityAuthorityTopicEmbeddingsVersionedItem)
- WebRef entities (RepositoryWebrefWebrefMustangAttachment, deprecated → UDR)

**Clicks (C)** — historical aggregates feed into scoring. See NavBoost below.

## Layer 2: Site-Level Quality (NSR / Qstar / Panda)

`siteAuthority` in CompressedQualitySignals: "converted from quality_nsr.SiteAuthority, applied in Qstar".

NSR (QualityNsrNsrData):
- `nsr`, `nsrVariance`, `priorAdjustedNsr`, `vlqNsr`
- `chromeInTotal` — site-level Chrome views
- `site2vecEmbedding`, `clusterId` (Tundra)
- `spambrainLavcScore`, `tofu`, `chardEncoded`
- `titlematchScore`, `localityScore`, `smallPersonalSite`

Panda / demotions (CompressedQualitySignals):
- `pandaDemotion`, `babyPandaDemotion`, `babyPandaV2Demotion`
- `exactMatchDomainDemotion`, `navDemotion`, `serpDemotion`, `anchorMismatchDemotion`
- `unauthoritativeScore`, `scamness` (0-1023)

Site quality patents (US9760641B1 / US9031929, Panda/Lehman):
- Ratio of reference queries (branded/navigational) to total associated queries.
- Implementations include threshold `T` so new sites start at zero until branded query count exceeds threshold.

Other site signals:
- `hostAge` (PerDocData) — 16-bit day number after 2005-12-31; used to sandbox fresh spam
- `homepagePagerankNs` / `homePageInfo` (PerDocData) — homepage trust level propagates
- `siteFocusScore` / `siteRadius` (QualityAuthorityTopicEmbeddingsVersionedItem) — topical concentration vs. deviation

## Layer 3: NavBoost Re-Ranking

Confirmed by Pandu Nayak under oath (DOJ 2023): one of the most important signals, ~13-month rolling window (was 18 months pre-2017). Eric Lehman: "Navboost is not a machine-learning system. It's just a big table."

Leak module: QualityNavboostCrapsCrapsClickSignals / CrapsData

| Field | Meaning |
|-------|---------|
| goodClicks | Engaged clicks (user stayed) |
| badClicks | Short clicks (user returned to SERP) |
| lastLongestClicks | Last and longest click in related user queries (documented) |
| impressions | Times shown |
| unicornClicks | Subset from Unicorn users |
| unsquashedClicks / unsquashedImpressions | Pre-normalization |

Slicing (QualityNavboostCrapsCrapsData):
- `country`, `language`, `device`, `sliceTag`
- `voterTokenCount` — privacy lower bound on distinct users
- `unscaledIpPriorBadFraction` — IP prior (craps-penalty.cc)
- `patternLevel` — 0=URL, higher=more general

Patents:
- US8595225B1 (2004, Singhal/Hoelzle) — correlating topicality and popularity via user interactions
- US8661029B1 / US10229166B1 — modifying ranking based on implicit user feedback; LC click fraction

NavBoost re-ranks after first-pass scoring. Signals are aggregated over the rolling window, sliced by locale/device.

## Layer 4: Content Quality & Originality

- `OriginalContentScore` (PerDocData) — 7-bit, only on thin pages; real range 0-512
- `contentEffort` (QualityNsrPQData) — `list(QualityNsrVersionedFloatSignal)`, "LLM-based effort estimation for article pages (see landspeeder/4311817)"
- `titlematchScore` (QualityNsrNsrData) — how well titles match queries

Information Gain (US11354342B2, Carbune/Gonnet, 2018/2022):
- Scores additional information in a document beyond documents already presented to the user.
- Session-level in the patent text; broader corpus application is inferred, not confirmed.
- Aligns with contentEffort and OriginalContentScore direction.

## Layer 5: Freshness

- `lastSignificantUpdate` (PerDocData) — UNIX timestamp from LSU Selector
- `syntacticDate` (CompositeDoc → QualityTimebasedSyntacticDate) — `bylineDate`, `trustSyntacticDateInRanking`, `useAsBylineDate`
- `hostAge` — sandbox for fresh spam
- `freshnessEncodedSignals` — deprecated

## Layer 6: Spam & Demotion

Anchor spam (IndexingDocjoinerAnchorSpamInfo / AnchorPhraseSpamInfo):
- `spamProbability`, `spamPenalty`
- Spike detection: `phraseAnchorSpam*` tagged LINK_SPAM_PHRASE_SPIKE
- Trusted source matching

Content spam (PerDocData):
- `IsAnchorBayesSpam`, `uacSpamScore` (threshold 64), `keywordStuffingScore`, `GibberishScore`
- `spamtokensContentScore` (used in SiteBoostTwiddler for UGC spam)

Site spam:
- `SpamBrainData.versionedData` — sitechunk level
- `spambrainLavcScore` (QualityNsrNsrData)

## ABC Summary (DOJ Exhibit)

Most signals except RankBrain and DeepRank are hand-crafted. Engineers fit curves on data + rater labels.

- **A** — Anchors (source → target, Reasonable Surfer weighted)
- **B** — Body (terms + embeddings)
- **C** — Clicks (NavBoost aggregates)

## What This Does Not Tell Us

- Exact weights or the final IR score formula.
- Which fields are currently active vs. deprecated vs. LE-only.
- Whether Information Gain is applied globally or only session-level.
- The precise interaction between NSR, Qstar, NavBoost, and embeddings.

## Practical Priorities (by evidence strength)

1. Earn `lastLongestClicks` — strongest documented positive NavBoost signal.
2. Avoid `badClicks`.
3. Build independent links + reference queries → lower Panda risk, higher siteAuthority.
4. Maintain topical focus (`siteFocusScore` high, `siteRadius` low).
5. Produce original effort (`contentEffort`, `OriginalContentScore`).
6. Contextual anchors (`pagerankWeight`, `fontsize`, sourceType).
7. Freshness hygiene (accurate byline, real lastSignificantUpdate).
8. Spam hygiene (no stuffing, no anchor spikes).

The schema shows capacity. The patents show mechanism. The DOJ testimony confirms NavBoost is central. The rest is testing.
