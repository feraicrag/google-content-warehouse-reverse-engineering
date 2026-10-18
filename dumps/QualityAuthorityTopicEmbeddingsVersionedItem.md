# QualityAuthorityTopicEmbeddingsVersionedItem

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityAuthorityTopicEmbeddingsVersionedItem.html

Header: Proto populated into shards and copied to superroot. Message storing a versioned TopicEmbeddings scores. Copied from TopicEmbeddings in docjoins.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| pageEmbedding | String.t | nil | — |
| siteEmbedding | String.t | nil | Compressed site/page embeddings. |
| siteFocusScore | number() | nil | Number denoting how much a site is focused on one topic. |
| siteRadius | number() | nil | The measure of how far page_embeddings deviate from the site_embedding. |
| versionId | integer() | nil | — |
