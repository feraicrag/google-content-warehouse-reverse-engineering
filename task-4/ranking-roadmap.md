# Ranking Roadmap — From Leak + Patents

This is a synthesis of verified leak fields, patent mechanisms, and DOJ testimony. It is not a claim of exact weights or that every field is active in production. It is a map of what Google has built the capacity to measure.

## Layer 1: Retrieval & First-Pass Scoring

- **Anchors (A)**: Reasonable Surfer weighted links. Optimize for contextual, in-content links from high-sourceType pages. `pagerankWeight`, `fontsize`, `locality` matter.
- **Body (B)**: Term matching + embeddings. `site2vecEmbedding`, `pageEmbedding`, WebRef entities (now UDR).
- **Clicks (C)**: Historical NavBoost aggregates feed into scoring.

## Layer 2: Site-Level Quality (NSR / Qstar)

- `siteAuthority` applied in Qstar. Build consistent topical focus (`siteFocusScore` high, `siteRadius` low).
- Earn independent links and reference queries (Panda ratio IL/RQ).
- Avoid `pandaDemotion`, `babyPandaDemotion`, `scamness`, `unauthoritativeScore`.
- `chromeInTotal` and `hostAge` exist; new sites face sandbox for fresh spam.
- `homepagePagerankNs` propagates from homepage.

## Layer 3: NavBoost Re-Ranking (13-month window)

- Maximize `goodClicks` and `lastLongestClicks`.
- Minimize `badClicks`.
- Signals are sliced by country, language, device (`sliceTag`, `mobileSignals`).
- `voterTokenCount` and IP priors filter manipulation.
- Effect compounds over the rolling window.

## Layer 4: Content Quality & Originality

- `OriginalContentScore` on thin pages.
- `contentEffort` (LLM-based) on article pages.
- Information Gain direction: add information beyond what the user has already seen (session or corpus).
- Align title with content (`titlematchScore`).
- Maintain topical coherence (`siteFocusScore` / `siteRadius`).

## Layer 5: Freshness & Dates

- `lastSignificantUpdate` from LSU Selector.
- `syntacticDate` with `trustSyntacticDateInRanking` and `useAsBylineDate`.
- `hostAge` for sandbox.

## Layer 6: Spam & Demotion Defense

- Anchor spam: avoid spikes (`phraseAnchorSpam*`), maintain trusted sources.
- Content spam: `keywordStuffingScore`, `GibberishScore`, `IsAnchorBayesSpam`, `uacSpamScore`.
- Site spam: `spambrainLavcScore`, `SpamBrainData.versionedData`.

## Practical Priorities (ordered by evidence strength)

1. **Earn lastLongestClicks** — strongest documented positive NavBoost signal. Satisfying, complete answers.
2. **Avoid badClicks** — short returns kill the ratio.
3. **Build site-level authority** — independent links + reference queries → lower Panda demotion risk, higher siteAuthority.
4. **Topical focus** — high siteFocusScore, low siteRadius. Don't dilute the site embedding.
5. **Original effort** — contentEffort and OriginalContentScore reward non-regurgitated work.
6. **Contextual anchors** — Reasonable Surfer still in the schema (`pagerankWeight`, `fontsize`).
7. **Freshness hygiene** — accurate byline dates, real updates that move lastSignificantUpdate.
8. **Spam hygiene** — no stuffing, no gibberish, no anchor spikes.

## What the Leak Does Not Tell Us

- Exact weights.
- Which fields are currently active vs. deprecated vs. LE-only.
- The precise formula that combines ABC + NSR + NavBoost + embeddings into the final score.
- Whether Information Gain is applied globally or only session-level.

Use the map. Test. Measure. The schema shows capacity, not the current production mix.
