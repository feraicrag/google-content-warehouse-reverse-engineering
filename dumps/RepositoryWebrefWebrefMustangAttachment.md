# RepositoryWebrefWebrefMustangAttachment

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.RepositoryWebrefWebrefMustangAttachment.html

**DEPRECATED.** See go/udr/migrate-wma. Legacy use allowed, no new usage accepted. UDR has same features.

Next available tag: 25

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| categoryConfidenceE2 | list(integer) | nil | Confidence of category. Range [0, 100]. |
| categoryEncodedMid | list(String) | nil | uint64-encoded MIDs of HitCat categories. See go/category-annotations-api. |
| confidenceE2 | list(integer) | nil | Confidence scores. Fixed-point /100. |
| encodedMid | list(String) | nil | int64-encoded MIDs sorted by topicality. |
| entityMetadata | list(RepositoryWebrefWebrefAttachmentMetadata) | nil | Per-entity metadata. Not packed. |
| iqlAttachment | KnowledgeAnswersIntentQueryIndexingIQLAttachment | nil | IQL expressions for Pianno. |
| isAuthorIndex | list(integer) | nil | Indices of author entities. |
| isPublisherIndex | list(integer) | nil | Indices of publisher entities. |
| referencePageIndex | list(integer) | nil | Indices when document is reference page for entity. |
| topicalityE2 | list(integer) | nil | Topicality scores. Fixed-point /100. |
| unboundIntentMid | list(String) | nil | uint64-encoded MID of unbound intents (Pianno). |
| unboundIntentScoreE2 | list(integer) | nil | Confidence of unbound intent. Range [0, 100]. |
