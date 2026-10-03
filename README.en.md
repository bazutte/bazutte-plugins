# Bazutte Plugins

[日本語](README.md) | [English](README.en.md)

Research YouTube videos and channels with [Bazutte](https://bazutte.com) from Claude, Claude Code, and Codex. The plugin bundles the MCP connection with a research skill for video discovery, competitor comparisons, and channel analysis.

## Requirements

- A paid Claude plan (Pro, Max, Team, or Enterprise), or Claude Code or Codex CLI.
- Git if installing through a CLI.
- A Bazutte account with permission to use the MCP service.
- Network access to GitHub and `https://bazutte.com/mcp`.

The plugin connects to Bazutte's production MCP endpoint. Installing or enabling it may initiate a connection or an authentication prompt.

## Quick start

### Claude (web and regular app)

1. Open [Claude's Plugins page](https://claude.ai/customize/plugins) and select **Add → Add marketplace**.
2. Enter `https://github.com/bazutte/bazutte-plugins` to add the marketplace, then add the **Bazutte** plugin it lists.
3. Open the plugin's **Connectors** tab. If Bazutte is not added yet, select **Add**, then **Connect**. Sign in to Bazutte and grant access.

No CLI installation or manual MCP URL entry is needed. For Team and Enterprise, an owner must add the Bazutte connector first. For a Free plan or an account without the plugin menu, select Claude on [Bazutte's AI integration page](https://bazutte.com/ai_integration) and open the manual setup details.

For Codex or Claude Code, install the AI's CLI on the same computer first. Run the three commands below in a terminal, then sign in to Bazutte in your browser. The app and CLI use the same setup.

### Codex (app, CLI, and IDE extension)

```bash
codex plugin marketplace add https://github.com/bazutte/bazutte-plugins.git --ref main
codex plugin add bazutte@bazutte-plugins
codex mcp login bazutte
```

The third command starts Bazutte OAuth authentication. Complete sign-in and consent, then reopen your Codex app, CLI, or IDE extension and start a new conversation. The server is named `bazutte`.

### Claude Code (app and CLI)

```bash
claude plugin marketplace add https://github.com/bazutte/bazutte-plugins.git#main
claude plugin install bazutte@bazutte-plugins
claude mcp login plugin:bazutte:bazutte
```

Run the third command in an interactive terminal. Complete sign-in and consent, then reopen Claude Code and start a new conversation. Use a local session in the app. If the login command is unavailable, open `/mcp` in a conversation and select **Authenticate** for `plugin:bazutte:bazutte`.

For ChatGPT, follow the connector instructions on [Bazutte's AI integration page](https://bazutte.com/ai_integration).

## Ask in plain language

After connecting, you can ask without knowing tool names:

```text
Use Bazutte to find the 10 most viewed videos published yesterday, with video and channel links.
```

```text
Use Bazutte to find growing videos from channels with no more than 3,000 subscribers.
```

```text
Use Bazutte to compare this YouTube channel with its competitors by views gained and posts published in the last 30 days.
```

The bundled `youtube-research` skill selects data and comparison metrics that match your question, then presents results with video and channel links. If you ask for content ideas, it separates observed patterns from hypotheses. Analysis uses Bazutte's stored data.

Ask in plain language. You can also invoke `/bazutte:youtube-research` in Claude Code or `$youtube-research` in Codex.

## Authentication and privacy

Each user signs in to Bazutte and grants access through OAuth. No shared API key, access token, personal information, or account data is included in the package. Publishing the connection definition does not grant access to Bazutte data.

The package contains manifests, connection settings, and skills written in natural language. It has no installation scripts or lifecycle hooks. Adding it from Claude's Plugins page does not require Git on your computer.

## Compatibility

| Client | Plugin manifest | MCP definition | Authentication |
| --- | --- | --- | --- |
| Claude (paid plan) | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json` (`http`) | Bazutte OAuth from the plugin's Connectors tab |
| Codex CLI | `plugins/bazutte/plugin.json` | `mcp.json` (`streamable-http`) | Bazutte OAuth |
| Claude Code | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json` (`http`) | Bazutte OAuth |

The connection definitions were checked with Codex CLI `0.160.0` and Claude Code `2.1.284`. These are tested versions, not minimum-version guarantees. The Claude UI instructions follow the official documentation; a live account connection has not been tested.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| The Git source cannot be fetched | Confirm GitHub is reachable and the repository has the `main` branch and the marketplace catalog. CLI installation also requires Git. |
| The plugin is not listed or enabled | Confirm the marketplace is named `bazutte-plugins` and the plugin ID is `bazutte@bazutte-plugins`. Check the client's installed plugins, then open a new session. |
| Authentication fails or the tool is unavailable | Check the bundled server's authentication state and your Bazutte account's permissions in the client's MCP settings. |
| An older manual setup duplicates the connection | Check it with `codex mcp get bazutte` or `claude mcp get bazutte`. If you no longer need that manual configuration, remove it with `codex mcp remove bazutte` or `claude mcp remove --scope user bazutte`, then install the plugin. |
| Weekly usage is exhausted | Ask for your remaining Bazutte usage and check the returned reset time. |

Contact [Bazutte through its public website](https://bazutte.com). Include the client version and a sanitized error message.

## Package structure

```text
.agents/plugins/marketplace.json         # Codex catalog / Codex用カタログ
.claude-plugin/marketplace.json          # Claude Code catalog / Claude Code用カタログ
plugins/bazutte/
  plugin.json                           # Portable manifest / 共通形式の定義
  mcp.json                              # Codex MCP settings / Codex用MCP設定
  .claude-plugin/plugin.json             # Claude Code manifest / Claude Code用の定義
  .mcp.json                             # Claude Code MCP settings / Claude Code用MCP設定
  skills/youtube-research/SKILL.md       # YouTube research / 動画・チャンネル調査
```

Both catalogs expose `bazutte@bazutte-plugins`. Client-specific MCP settings point to the same production endpoint.

## Updates

Use your client's marketplace and plugin update controls to fetch a new release. For marketplaces added from Claude's Plugins page, select **Check for updates**. GitHub marketplaces also support **Sync automatically**. Automatic updates for custom Claude Code marketplaces are off by default; users can enable them in the marketplace settings.

For Claude Code, run `claude plugin marketplace update bazutte-plugins`, followed by `claude plugin update bazutte@bazutte-plugins`. For Codex, run `codex plugin marketplace upgrade bazutte-plugins`. Start a new conversation after updating.

## Release status

Version `0.2.0` adds a YouTube research skill. Once it reaches the distribution repository's `main` branch, use the update commands above to get it.

See [CHANGELOG.md](CHANGELOG.md) for release notes. The distribution repository provides user-facing files on `main` and version tags.

## References

- [Codex plugin packaging and distribution](https://developers.openai.com/plugins/build/plugins)
- [Claude plugin installation](https://claude.com/docs/plugins/overview)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code marketplace hosting and updates](https://code.claude.com/docs/en/plugins/host-marketplace)
