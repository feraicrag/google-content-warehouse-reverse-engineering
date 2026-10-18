# SpamBrainData

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.SpamBrainData.html

Header: Holds SpamBrain values populated in docjoins. Populated at sitechunked host level and sitechunked domain level in doc_attachments, saved in Perdocdata in respective fields.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| site | String.t | nil | Sitechunker site granularity for this result. |
| versionedData | list(SpamBrainScore) | nil | Versioned scores of SB classifiers. |
