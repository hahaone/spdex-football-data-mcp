# 工具说明 / Tools

以下十个工具均为只读，完整参数见服务返回的 `tools/list`。

| 工具 | 用途 / Purpose | 主要参数 |
| --- | --- | --- |
| `list_competitions` | 五大联赛赛程目录 / Fixture competitions | 无 |
| `list_seasons` | 已存赛季与阶段 / Stored seasons and stages | `competition_id`，`limit`，`cursor` |
| `search_teams` | 按来源搜索球队 / Search teams by source | `query`，`source`，`stage_id`，`limit`，`cursor` |
| `get_team_profile` | 球队档案 / Team profile | `team_id`（catalog） |
| `get_venue` | 球队档案关联球场 / Recorded team venue | `team_id`（catalog） |
| `get_team_squad` | 存档阵容 / Archived squad | `team_id`（squad），`limit`，`cursor` |
| `get_fixtures` | 阶段赛程 / Stage fixtures | `stage_id`，可选 `team_id`（catalog），`limit`，`cursor` |
| `get_match_results` | 历史纯比分 / Historical scores | `query`，`date_from`，`date_to`，`limit`，`cursor` |
| `get_team_availability` | 已存伤停报告 / Stored availability reports | `team_id`（availability），`limit`，`cursor` |
| `get_data_coverage` | 能力与限制 / Capabilities and limitations | 无 |

## 查询规则

- 分页默认 20 条，`limit` 范围 1–100。`has_more=true` 时使用 `next_cursor` 继续，包括空页；保持筛选、页长和用户身份不变。游标八分钟到期，到期或服务重启后从首页重新查询。
- 球队 ID 使用 `search_teams` 返回的原值，不同来源不能混用。`source=catalog` 用于档案、球场和赛程，需先取得 `stage_id`；`squad` 用于阵容，`availability` 用于伤停。阵容及伤停 ID 失效时重新搜索。
- 伤停搜索可能连续返回空页，建议从 `limit=100` 开始，直到 `has_more=false` 才算扫描完成。同一来源 ID 去重；不同 ID 的同名球队保留，报告可能不同。
- 单阶段赛程最多 500 场。历史比分从 2021-01-01 起，日期为 `YYYY-MM-DD`，不晚于北京时间当天，范围最多 366 天；每次读取七天窗口的一页。关键词使用赛事或球队名称。
- `fresh` 仅说明来源时间较近，不代表事实已核验。请保留来源时间和提示；存档阵容不保证当前效力关系，伤停空名单不代表全员健康。`score_basis=source_unspecified` 时不推断常规时间、加时或点球结果。

## 返回与错误

结果位于 `data.items`。`meta` 包含 `coverage_status`、`source_status`、`freshness`、`has_more`、`next_cursor` 和 `warnings`；具体记录可含 `source_updated_at`，未知时为空。工具失败时 `isError=true`，详情见 `error.code`、`error.message`，不能当作空结果。

| 情况 | 处理 |
| --- | --- |
| HTTP 401 | 检查或更换 Token |
| HTTP 403 | 检查客户端配置，联系支持 |
| HTTP 429 / `source_busy` | 降低频率，稍后重试 |
| `invalid_argument` / `cursor_mismatch` | 修正参数或从首页重新查询 |
| `cursor_expired` | 从首页重新查询，按结果 ID 去重 |
| `source_timeout` / `source_unavailable` | 稍后重试；持续失败联系支持 |
| `source_access_denied` / `source_unconfigured` | 联系支持 |
| `coverage_limit` | 当前范围超出覆盖限制 |

## English

Pages default to 20 items (1–100). Follow `next_cursor` while `has_more=true`, including empty pages; keep filters, page size and identity unchanged. Cursors expire after eight minutes or a service restart. Restart the query after expiry.

Use team IDs returned by search. Catalog queries require a `stage_id`; squad and availability IDs are separate and must be searched again if expired. Availability search may return consecutive empty pages: start with `limit=100` and continue until `has_more=false`. Exact IDs are deduplicated; same-name teams with different IDs remain separate.

Fixtures support up to 500 matches per stage. Historical queries start at 2021-01-01, use `YYYY-MM-DD` dates through the current day in Beijing time, and span up to 366 days. Each call reads one page of a seven-day window. Search by competition or team name.

Items are in `data.items`; coverage, freshness and pagination fields are under `meta`. Record timestamps may be null. Freshness reflects source time, not independent verification. Archived squads may be outdated; an empty availability list does not establish health. An unspecified scoring basis does not establish regulation-time, extra-time or penalty results. Errors use `isError=true` with `error.code/message`; they are not successful empty results.
