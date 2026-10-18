# Actionable Ranking Checklist

Derived from verified hexdocs 0.4.0 fields + patents + DOJ testimony.

## Limits (read first)

- NavBoost aggregates over ~13 months (Pandu Nayak, DOJ 2023). One day of clicks does not move the rolling window.
- siteAuthority is converted from quality_nsr.SiteAuthority and applied in Qstar. It is a site-level signal.
- The schema shows capacity. It does not show weights, active vs. deprecated status, or a 1-day formula.
- Information Gain (US11354342B2) is session-level in the patent text.

## Priority 1 — NavBoost (click satisfaction)

| Signal | Field | Action |
|--------|-------|--------|
| Earn last longest clicks | lastLongestClicks | Pages that fully answer the query and end the search session. Complete, self-contained answers. |
| Avoid short returns | badClicks | Reduce bounce-back. Match title/snippet to actual content. No bait. |
| Engaged clicks | goodClicks | Content that holds attention. |
| Slice awareness | country / language / device | Signals are sliced. Mobile and desktop are separate pools. |
| Privacy floor | voterTokenCount | Distinct users matter. Single-IP or low-diversity traffic is filtered. |

## Priority 2 — Site-level quality (NSR / Qstar / Panda)

| Signal | Field | Action |
|--------|-------|--------|
| Site authority | siteAuthority | Build independent links and reference queries. Avoid Panda demotion fields. |
| Topical focus | siteFocusScore / siteRadius | High focus, low radius. Do not dilute the site embedding with off-topic pages. |
| Chrome views | chromeInTotal | Site-level Chrome data exists. Public denials were contradicted. |
| Host age | hostAge | New sites face sandbox for fresh spam. |
| Homepage trust | homepagePagerankNs / homePageInfo | Homepage trust level propagates. |
| Title match | titlematchScore | Titles that match queries. |
| Predicted default | predictedDefaultNsr | Fallback when no direct NSR. |

## Priority 3 — Link graph (Reasonable Surfer)

| Signal | Field | Action |
|--------|-------|--------|
| Per-link weight | pagerankWeight | Contextual, in-content links. Font size and position matter (fontsize, offset). |
| Source quality | sourceType | HIGH < MEDIUM < LOW. Links from base-tier pages carry more. |
| Locality | locality / bucket | Quality measure of the anchor. |
| Anchor spam | spamProbability / phraseAnchorSpam* | Avoid spikes. LINK_SPAM_PHRASE_SPIKE tags demote. |

## Priority 4 — Content quality

| Signal | Field | Action |
|--------|-------|--------|
| Original content | OriginalContentScore | Non-thin pages. Real range 0-512. |
| Effort | contentEffort | LLM-based effort estimation for article pages (landspeeder/4311817). |
| Information gain | US11354342B2 | Add information beyond what the user has already seen (session-level in patent). |

## Priority 5 — Freshness

| Signal | Field | Action |
|--------|-------|--------|
| Last significant update | lastSignificantUpdate | Real updates that move the LSU timestamp. |
| Byline date | syntacticDate / useAsBylineDate | Accurate dates. trustSyntacticDateInRanking for high-confidence non-byline. |

## Priority 6 — Spam hygiene

| Signal | Field | Action |
|--------|-------|--------|
| Anchor bayes | IsAnchorBayesSpam | Avoid patterns that trigger. |
| UAC spam | uacSpamScore | Threshold 64. |
| Stuffing / gibberish | KeywordStuffingScore / GibberishScore | Clean content. |
| SpamBrain | spambrainData / spambrainLavcScore | Sitechunk-level classifiers. |

## What a 1-day push can do

- Fix title/snippet mismatch that generates badClicks.
- Remove thin or stuffed pages that hit OriginalContentScore / KeywordStuffingScore.
- Align new pages to site embedding (siteFocusScore / siteRadius).
- Ensure byline dates and lastSignificantUpdate are accurate.
- Add contextual anchors from high-sourceType pages.

## What a 1-day push cannot do

- Move the 13-month NavBoost window.
- Create siteAuthority from zero.
- Override hostAge sandbox for fresh spam.
- Guarantee ranking. The schema shows what can be measured, not the current production mix.

Test. Measure. The fields are the map. The weights are not in the leak.
