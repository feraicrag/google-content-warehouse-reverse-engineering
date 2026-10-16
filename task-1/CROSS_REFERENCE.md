# Cross-reference: leak field ↔ patent ↔ DOJ ↔ circulating analysis

| Leak field / module | Patent / official system | DOJ / testimony | Circulating analysis | Status |
|---|---|---|---|---|
| goodClicks / badClicks / lastLongestClicks (CrapsClickSignals) | US11816114B1 family (implicit user feedback); Reasonable Surfer click-probability lineage | NavBoost ~13-mo rolling clicks (Nayak); ABC = Anchors/Body/Clicks | iPullRank, SparkToro, BeCited | CONFIRMED in hexdocs v0.4.0 |
| siteAuthority (CompressedQualitySignals) | US9031929B1 (site quality score via branded/nav queries) | — | iPullRank (contradicts Mueller/Ilyes) | CONFIRMED |
| siteFocusScore / siteRadius (TopicEmbeddingsVersionedItem) | topical clustering / entity patents; US11354342B2 (info gain) | — | iPullRank | CONFIRMED, but WRONG MODULE in Wikipedia |
| OriginalContentScore (PerDocData) | US11354342B2 (information gain); Quality Rater Guidelines | — | multiple | CONFIRMED |
| homepagePagerankNs / homePageInfo (PerDocData) | PageRank variants; site quality inheritance | — | BeCited | CONFIRMED in PerDocData |
| chromeInTotal (NSR data) | Chrome-derived popularity patents | Mueller/Cutts denials | iPullRank, BeCited | CONFIRMED |
| hostAge (PerDocData) | US7346839B2 (historical data / spam) | Mueller sandbox denial | BeCited | CONFIRMED |
| contentEffort (LLM effort est.) | Quality Rater "effort" emphasis | — | BeCited, Willie Jiang | NOT FOUND in hexdocs v0.4.0 — unconfirmed |
| spam* scores (PerDocData) | SpamBrain / phrase-spam patents | — | iPullRank | CONFIRMED |
| site2vecEmbedding(s) (NSR) | site2vec / embeddings patents | — | iPullRank | CONFIRMED |
| Panda demotions (CQS) | Panda patents / Baby Panda | — | iPullRank | CONFIRMED |

## Interpretation rule (Task 20)

A field is **CONFIRMED STORED** if present in hexdocs v0.4.0 with a description. It is **CONFIRMED USED IN RANKING** only if additionally supported by DOJ testimony or official systems docs. Storage ≠ live weight.
