# QualityAuthorityTopicEmbeddingsVersionedItem (hexdocs v0.4.0)

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityAuthorityTopicEmbeddingsVersionedItem.html

5 fields:

- `pageEmbedding` (string)
- `siteEmbedding` (string) — "Compressed site/page embeddings"
- `siteFocusScore` (number) — **"Number denoting how much a site is focused on one topic"**
- `siteRadius` (number) — **"The measure of how far page_embeddings deviate from the_site_embedding"**
- `versionId` (integer)

Module description (verbatim): "Proto populated into shards and copied to superroot. Message storing a versioned TopicEmbeddings scores. This is copied from TopicEmbeddings in docjoins."

## Correction vs circulating analyses

Wikipedia and several SEO summaries state siteFocusScore/siteRadius live in QualityNsrNsrData. **They do not.** They live here. This is the single most important structural correction from Task 1 primary-source verification.

See also: CORRECTIONS.md.
