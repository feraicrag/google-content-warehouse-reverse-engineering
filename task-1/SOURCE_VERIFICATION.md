# Task 1.1 — Source Verification

## The leak event

| Item | Value |
|------|-------|
| Source repo | `googleapis/elixir-google-api` (archived 2026-06-30, read-only) |
| Bot | `yoshi-code-bot` (automated regeneration via PR generator) |
| Addition commit | `d7a637fceb1011ee26e094029ce67e6b6778220` |
| Addition date | 2024-03-13 03:02 UTC |
| Addition message | "feat: Automated regeneration of ContentWarehouse client (#11021)" |
| Addition stats | 2,596 files changed, 178,764 insertions, 0 deletions |
| Addition parent | `35bfb58` |
| Removal commit | `078b497fceb1011ee26e094029ce67e6b6778220` |
| Removal date | 2024-05-07 |
| Removal stats | 2,423 files changed, 7 insertions, 164,707 deletions |
| External cache | hexdocs `google_api_content_warehouse` v0.4.0 (Apache 2.0) |
| Hexdocs base | https://hexdocs.pm/google_api_content_warehouse/0.4.0/ |
| Total modules | 2,596 |
| Total attributes | 14,014 |

## Verification steps performed

1. Located both commits via GitHub (still accessible; repo archived but commits readable).
2. Confirmed addition commit author = yoshi-code-bot, message references PR #11021, generated with toys PR generator.
3. Confirmed removal commit on May 7, 2024.
4. Confirmed hexdocs v0.4.0 still live and serving the full schema.
5. Cross-checked module/attribute totals against Wikipedia and BeCited summaries (both state 2,596 / 14,014).
6. Opened primary model pages on hexdocs and extracted fields verbatim.

## Notes

- The addition commit date (March 13) differs from some reports citing March 27. The commit SHA and stats are authoritative; treat March 13 as the push date.
- Rand Fishkin's SparkToro post and Mike King's iPullRank post were published May 27–28, 2024, after the removal.
- Google's response (May 29) did not deny authenticity; spokespersons (Gary Illyes, John Mueller) argued the docs are "out of context" / "ingredients, not the recipe" — i.e., stored features, not confirmed live weights.
