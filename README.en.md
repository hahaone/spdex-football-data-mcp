# SPdex Football Data MCP

[中文](README.md) · [Tools](docs/tools.md) · [Request access](docs/access.md) · [Privacy](docs/privacy.md) · [Terms](docs/terms.md)

Query football fixtures, historical scores, teams, venues, archived squads and availability reports through MCP-compatible clients. Ten read-only tools include coverage and freshness labels.

## Connect

1. Request an individual token through [SPdex support](https://help.spdex.com/support), QQ 2735629769.
2. Use endpoint `https://football-mcp.spdex.com/mcp`, transport **Streamable HTTP**, and header `Authorization: Bearer <your token>`.
3. In VS Code, merge [this configuration](configs/vscode.mcp.json) and enter the token through the password input. Keep existing server settings and do not publish credentials.

Access is free during the preview. See [access instructions](docs/access.md) for places, rate limits and token validity. Call `get_data_coverage` to check coverage.

## Example queries

- Find Arsenal fixtures in the 2026–2027 Premier League season.
- Look up World Cup scores on 2022-12-18.
- Show Arsenal's archived squad and availability reports with update times.

Fixtures cover stored stages of the five major European leagues. Historical scores start in 2021. Records may be missing or stale; coverage is not guaranteed complete or live. Check the returned notes on scoring basis, squads and availability.

Provider: 北京枫诚创业科技有限公司 (SPdex). This repository provides documentation and client configuration for the SPdex-hosted service. Public materials use the [MIT licence](LICENSE-STATUS.md).
