# QualityNsrPQData

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityNsrPQData.html

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| chard | integer() | nil | URL-level chard prediction (encoded as an int). |
| chardScoreEncoded | list(QualityNsrVersionedIntSignal) | nil | URL-level Chard (encoded as an int). |
| **contentEffort** | list(QualityNsrVersionedFloatSignal) | nil | **LLM-based effort estimation for article pages (see landspeeder/4311817).** |
| deltaAutopilotScore | number() | nil | — |
| deltaLinkIncoming | number() | nil | — |
| deltaLinkOutgoing | number() | nil | — |
| deltaSubchunkAdjustment | number() | nil | Total deltaNSR adjustment based on subchunks. Page-level adjustment. |
| keto | list(QualityNsrVersionedFloatSignal) | nil | Keto score. |
| linkIncoming | number() | nil | — |
| linkOutgoing | number() | nil | — |
| numOffdomainAnchors | number() | nil | Total number of offdomain anchors seen by the NSR pipeline for this page. |
| page2vecLq | number() | nil | — |
| predictedDefaultNsr | list(QualityNsrVersionedFloatSignal) | nil | Predicted default NSR score computed in Goldmine via the NSR default predictor (go/default-nsr-predictor). |
| rhubarb | list(QualityNsrVersionedFloatSignal) | nil | Site-URL delta signals based quality score computed in Goldmine via the Rhubarb model (go/rhubarb-dd). |
| subchunkData | list(QualityNsrPQDataSubchunkData) | nil | — |
| tofu | number() | nil | URL-level tofu prediction. |
| unversionedRhubarb | number() | nil | The delta score of the URL-level quality predictor. |
| urlAutopilotScore | number() | nil | — |
| vlq | number() | nil | URL-level score of the VLQ model. |
