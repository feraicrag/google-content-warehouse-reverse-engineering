# AnchorsAnchor

Source: https://hexdocs.pm/google_api_content_warehouse/0.4.0/GoogleApi.ContentWarehouse.V1.Model.AnchorsAnchor.html

Key ranking-related fields:

| Field | Type | Description |
|-------|------|-------------|
| pagerankWeight | number() | Weight to be stored in linkmaps for pageranker |
| fontsize | integer() | — |
| locality | integer() | For ranking purposes, quality measured by locality and bucket. See quality/anchors/definitions.h |
| bucket | integer() | — |
| sourceType | integer() | Quality of source page. TYPE_HIGH_QUALITY (base docs) < TYPE_MEDIUM_QUALITY (supplemental) < TYPE_LOW_QUALITY (blackhole). TYPE_FRESHDOCS treated as HIGH for importance. |
| context2 | integer() | Hash of terms near the anchor (second-generation) |
| isLocal | boolean() | Roughly indicates source and target on same domain. Does not determine onsite/ondomain/offdomain in mustang. |
| firstseenDate | integer() | Days past 1994-12-31 23:00 UTC. Max 15 bits. |
| creationDate | integer() | First/last time seen. Used for Freshdocs Twitter. |
| parallelLinks | integer() | Additional links from same source page to same target domain. Not populated if is_local. |
| linkTags | list(integer) | Link type, source page, etc. |
| catfishTags | list(integer) | CATfish tags, created on the fly in Cookbook. |
| experimental | boolean() | If true, should not be used in serving. |
| offset | integer() | Offset of first term in anchor (bytes). Unique ID within document. |

sourceType correlation with index tier is approximate, not identical.
