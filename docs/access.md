# 足球资料 MCP 接入 / Access

1. 登录 [SPdex 足球资料 MCP](https://new.spdex.com/account/football-mcp)，阅读条款并领取专用 Token。
2. 在同一页面复制客户端配置。VS Code 使用密码输入框；其他客户端按页面说明填写 Token。
3. 启用连接后，应发现 10 个只读工具。调用 `get_data_coverage` 检查资料范围。

**足球资料专用 Token 与主站“AI 与 MCP 连接”生成的业务 Token 不通用。** Agensi Skill 保持免费，安装 Skill 不会自动开通服务，也不包含共享 Token。

| 项目 | 免费预览 |
| --- | --- |
| 费用 | 免费，不扣业务 MCP 用量，不自动收费 |
| 名额 | 20 个有效用户账户，每账户一枚有效 Token |
| 频率 | 每账户每分钟 60 次请求，多客户端共享 |
| 有效期 | 领取起 30 天，页面显示到期时间 |
| 换发与撤销 | 在开通页面操作；换发立即使旧 Token 失效，不自动续期 |

Token 明文只展示一次，请直接保存到自己的客户端；丢失时换发。不要放入 AI 对话、公开 Issue、截图或代码仓库。原人工领取的有效 Token 可继续使用至到期或撤销。

- **401**：确认使用足球资料专用 Token，检查有效期；换发后更新客户端并重新连接。
- **429**：请求过于频繁，稍后重试。
- **503**：服务暂时不可用，稍后重试，不要反复换发。
- **OAuth/client ID 提示**：本服务使用 Bearer Token，取消提示并检查客户端配置。

[使用条款](terms.md) · [隐私说明](privacy.md) · [联系支持](https://help.spdex.com/support)

## English

Sign in to the [SPdex Football Data MCP page](https://new.spdex.com/account/football-mcp), accept the terms and generate a dedicated token. Copy the client configuration from that page, then call `get_data_coverage` to verify access to the ten read-only tools.

**Business MCP tokens generated under “AI and MCP connections” do not work with Football Data MCP.** The Agensi skill remains free; using it does not grant service access or provide a shared token.

Free preview: 20 active user accounts, one active token per account, 60 requests per minute shared across clients, valid for 30 days. No business MCP credits are deducted and there is no automatic charge or renewal. Rotate or revoke the token on the same page; rotation immediately invalidates the old token. Existing manually issued tokens remain valid until expiry or revocation.

The token is shown once. Save it in your client, never in chat, public issues, screenshots or source control. For 401, check the token type and expiry; for 429 or 503, retry later. Cancel OAuth/client-ID prompts and use Bearer authentication. See the [terms](terms.md), [privacy notice](privacy.md) or [support](https://help.spdex.com/support).
