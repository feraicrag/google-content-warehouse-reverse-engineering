# CompositeDoc

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.CompositeDoc.html

Master container. Key fields for ranking analysis:

| Field | Type | Notes |
|-------|------|-------|
| perDocData | PerDocData | Main per-document signals |
| anchors | Anchors | Anchor graph |
| properties | DocProperties | Title, languages, token counts |
| syntacticDate | QualityTimebasedSyntacticDate | Byline / syntactic date |
| qualitysignals | CompositeDocQualitySignals | — |
| anchorStats | IndexingDocjoinerAnchorStatistics | Aggregated anchor stats |
| porninfo | ClassifierPornDocumentData | Porn classification |
| docAttachments | Proto2BridgeMessageSet | Generic annotations |
| richsnippet | RichsnippetsPageMap | Extracted rich snippet |
| localizedAlternateName | list | Webmaster-provided localized alternates |
| urldate | String | Date extracted from URL |
| registrationinfo | RegistrationInfo | Domain creation/expiration |

Full field list extracted from hexdocs (partial update info, checksums, videos, images, indexing intermediate, etc.). See source for complete set.
