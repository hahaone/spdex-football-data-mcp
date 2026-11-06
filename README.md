# SPdex足球资料MCP

[English](README.en.md) · [工具说明](docs/tools.md) · [申请 Token](docs/access.md) · [隐私说明](docs/privacy.md) · [使用条款](docs/terms.md)

通过兼容 MCP 的客户端查询足球赛程、历史比分、球队、球场、存档阵容及伤停报告。提供十个只读工具，附覆盖范围和时效标记。

## 接入

1. 登录 [足球资料 MCP 开通页](https://new.spdex.com/account/football-mcp)，领取专用 Token 和客户端配置。主站业务 MCP Token 不适用。
2. 配置服务地址 `https://football-mcp.spdex.com/mcp`，传输方式 **Streamable HTTP**，认证头 `Authorization: Bearer <你的 Token>`。
3. VS Code 用户可合入 [配置文件](configs/vscode.mcp.json)，通过密码框输入 Token。请保留已有配置，不要公开凭据。

免费试用，名额、频率和有效期见[接入说明](docs/access.md)。连接后可调用 `get_data_coverage` 查看覆盖范围。

## 查询示例

- 查询 2026—2027 英超赛程中阿森纳的比赛。
- 查询 2022 年 12 月 18 日世界杯比分。
- 查询 Arsenal 的存档阵容和伤停报告，注明更新时间。

赛程提供五大联赛的已存阶段，历史比分从 2021 年起。资料可能缺失或陈旧，不保证实时或完整；比分口径、阵容和伤停状态以返回说明为准。

服务提供者：北京枫诚创业科技有限公司（SPdex）。本仓库提供文档和客户端配置，服务由 SPdex 托管。公开材料采用 [MIT 许可](LICENSE-STATUS.md)。
