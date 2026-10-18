# Corrections

## contentEffort — REVERSED (2026-10-18)

Previous Task 1 claim that contentEffort was NOT FOUND in hexdocs 0.4.0 is incorrect.

**Confirmed location:** `GoogleApi.ContentWarehouse.V1.Model.QualityNsrPQData`

- **Field:** `contentEffort`
- **Type:** `list(GoogleApi.ContentWarehouse.V1.Model.QualityNsrVersionedFloatSignal.t)`
- **Default:** `nil`
- **Description (literal):** "LLM-based effort estimation for article pages (see landspeeder/4311817)."

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.QualityNsrPQData.html

## siteFocusScore / siteRadius module location

Wikipedia and some secondary analyses placed these in QualityNsrNsrData. Primary source places them in `QualityAuthorityTopicEmbeddingsVersionedItem`.

## homepagePagerankNs / homePageInfo

Located in PerDocData, not CompressedQualitySignals.
