# Corrections to circulating analyses (Task 1)

## 1. siteFocusScore / siteRadius module (HIGH)

**Claim:** Wikipedia and SEO summaries place siteFocusScore and siteRadius inside QualityNsrNsrData.

**Primary source (hexdocs v0.4.0):** Both fields live in `GoogleApi.ContentWarehouse.V1.Model.QualityAuthorityTopicEmbeddingsVersionedItem`, a 5-field proto (pageEmbedding, siteEmbedding, siteFocusScore, siteRadius, versionId) described as "Proto populated into shards and copied to superroot."

**Impact:** Anyone building tooling or mental models off the Wikipedia placement is targeting the wrong module. The TopicEmbeddings proto is what gets copied to superroot — which is arguably the more operationally important location.

## 2. homepagePagerankNs / homePageInfo location (MEDIUM)

**Claim:** Some summaries imply these live in CompressedQualitySignals.

**Primary source:** They are fields of PerDocData.

## 3. contentEffort (MEDIUM)

**Claim:** BeCited and others cite "contentEffort — LLM-based effort estimation for article pages" as a leak field.

**Primary source check:** Not found in PerDocData, CompressedQualitySignals, QualityNsrNsrData, NavBoost Craps, or TopicEmbeddings modules opened in Task 1. Either it lives in an unopened module or the circulating description is imprecise. → tracked in UNCONFIRMED.md.

## 4. Addition commit date (LOW)

Some reports say March 27. Commit d7a637f is dated March 13, 2024 03:02 UTC. SHA is authoritative.
