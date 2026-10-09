# Bazutte Plugins

[日本語](README.md) | [English](README.en.md)

Research YouTube videos and channels using [Bazutte](https://bazutte.com)'s stored data from Claude, Claude Code, and Codex. This plugin is provided by Bazutte and bundles the MCP connection with a research skill for video discovery, competitor comparisons, and channel analysis.

Data sources include YouTube API Services. The MCP returns stored information and Bazutte's own metrics in Bazutte's format. This is not an official YouTube plugin or a general-purpose client for calling the YouTube Data API directly. YouTube is a trademark of Google LLC.

## Requirements

- A paid Claude plan (Pro, Max, Team, or Enterprise), or Claude Code or Codex CLI.
- Git if installing through a CLI.
- A Bazutte account with permission to use the MCP service.
- Network access to GitHub and `https://bazutte.com/mcp`.

The plugin connects to Bazutte's production MCP endpoint. Installing or enabling it may initiate a connection or an authentication prompt.

## Quick start

The Bazutte plugin is not yet listed in any AI's official directory. Add the GitHub repository `bazutte/bazutte-plugins` as a marketplace, then install Bazutte from it.

### Claude (web and regular app)

1. Open [Claude's Plugins page](https://claude.ai/customize/plugins) and select **Add → Add marketplace**.
2. Enter `https://github.com/bazutte/bazutte-plugins` to add the marketplace, then add the **Bazutte** plugin it lists.
3. Open the plugin's **Connectors** tab. If Bazutte is not added yet, select **Add**, then **Connect**. Sign in to Bazutte and grant access.

No CLI installation or manual MCP URL entry is needed. The plugin also syncs to the Claude apps and Claude Code signed in to the same account. For Team and Enterprise, an owner must add the Bazutte connector first. For a Free plan or an account without the plugin menu, select Claude on [Bazutte's AI integration page](https://bazutte.com/ai_integration) and open the manual setup details.

For Codex or Claude Code, install the AI's CLI on the same computer first. Run the commands below in a terminal, then sign in to Bazutte in the browser that the last command opens. The app and CLI use the same setup.

### Codex (app, CLI, and IDE extension)

```bash
codex plugin marketplace add bazutte/bazutte-plugins
codex plugin add bazutte@bazutte-plugins
codex mcp login bazutte
```

The third command starts Bazutte OAuth authentication. Complete sign-in and consent, then reopen your Codex app, CLI, or IDE extension and start a new conversation. The server is named `bazutte`.

### Claude Code (app and CLI)

```bash
claude plugin install bazutte --marketplace bazutte/bazutte-plugins
claude mcp login plugin:bazutte:bazutte
```

The first command adds the marketplace and installs the plugin. If it fails, update Claude Code with `claude update`. Run the second command in an interactive terminal. Complete sign-in and consent, then reopen Claude Code and start a new conversation. Use a local session in the app. If the login command is unavailable, open `/mcp` in a conversation and select **Authenticate** for `plugin:bazutte:bazutte`.

ChatGPT cannot add a GitHub marketplace from its interface, so register the MCP URL instead. Follow the instructions on [Bazutte's AI integration page](https://bazutte.com/ai_integration). To also use the research skill, install the plugin with the Codex steps above.

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

```text
Use Bazutte to find the 100 most viewed videos published yesterday from channels with no more than 3,000 subscribers. Show thumbnails, spreading rate, and hit score, and save every returned field in a report.
```

The bundled `bazutte-research` skill selects data and comparison metrics that match your question, then presents results with source attribution and YouTube video and channel links. If you ask for content ideas, it separates observed patterns from hypotheses. Data update times and retrieval times are distinguished; real-time values are not guaranteed.

Ask in plain language. You can also invoke `/bazutte:bazutte-research` in Claude Code or `$bazutte-research` in Codex.

## Available research and reports

You can research video rankings, channel comparisons and details, past uploads, video metric history, keyword rankings, channel name changes, and stored ban and reinstatement history. Ask "What can Bazutte do?" for examples based on the connected tools' descriptions. Date ranges, limits, and permissions vary by tool.

When you ask to save every field, the skill avoids selecting a subset of columns and preserves the returned rows, fields, conditions, and warnings. It retrieves and saves the server's HTML report when supported, or builds a report from the retrieved data otherwise. Server reports are temporary; resource reading and file saving also depend on your AI client. "Every field" refers to the retrieved data, not every record stored in Bazutte.

Returned thumbnails use external image URLs and retain links to the original videos. Image links are provided when images cannot be displayed. Spreading rate, buzz score, and hit score are Bazutte's own multiplier metrics, not official YouTube metrics or ratings. A hit score of `1.0` can also be a fallback when the score cannot be calculated.

Reports are snapshots of retrieved information. Saving, embedding offline images, and redistributing data are subject to applicable terms and refresh or deletion requirements. Saving a report does not grant indefinite retention or redistribution rights. A server report's expiry is the deadline for accessing that temporary resource, not a data license expiry.

## Authentication and privacy

Each user signs in to Bazutte and grants access through OAuth. No shared API key, access token, personal information, or account data is included in the package. Publishing the connection definition does not grant access to Bazutte data.

Before use, review and agree to the [Bazutte Terms of Service](https://info.bazutte.com/terms) and [Privacy Policy](https://info.bazutte.com/privacy). The [YouTube Terms of Service](https://www.youtube.com/t/terms) also apply, and users must agree to them. See the [Google Privacy Policy](https://policies.google.com/privacy) for Google's data practices.

Tool arguments, including search conditions and identifiers, are sent to Bazutte. Results, including video and channel information, metrics, and reports, are passed to the AI client you use. Check that service's settings, terms, and privacy policy for its storage, sharing, and model-improvement practices. Authorizing a Bazutte connection does not authorize operations on your YouTube account or access to private YouTube analytics.

To disconnect, remove or disconnect Bazutte in your AI client's MCP or Connectors settings. Disconnecting does not necessarily delete conversations or saved reports held by the AI service. Follow that service's deletion procedures for its history and saved files. For Bazutte data inquiries or deletion requests, use the contact listed in its Privacy Policy.

The package contains manifests, connection settings, and skills written in natural language. It has no installation scripts or lifecycle hooks. Adding it from Claude's Plugins page does not require Git on your computer.

## Compatibility

| Client | Plugin manifest | MCP definition | Authentication |
| --- | --- | --- | --- |
| Claude (paid plan) | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json` (`http`) | Bazutte OAuth from the plugin's Connectors tab |
| Codex CLI | `plugins/bazutte/plugin.json` | `mcp.json` (`streamable-http`) | Bazutte OAuth |
| Claude Code | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json` (`http`) | Bazutte OAuth |

The install commands were checked with Codex CLI `0.162.0` and Claude Code `2.1.295`. These are tested versions, not minimum-version guarantees. The Claude UI instructions follow the official documentation; a live account connection has not been tested.

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
  skills/bazutte-research/SKILL.md        # Bazutte research / 動画・チャンネル調査
```

Both catalogs expose `bazutte@bazutte-plugins`. Client-specific MCP settings point to the same production endpoint.

## Updates

Use your client's marketplace and plugin update controls to fetch a new release. For marketplaces added from Claude's Plugins page, select **Check for updates**. GitHub marketplaces also support **Sync automatically**. Automatic updates for custom Claude Code marketplaces are off by default; users can enable them in the marketplace settings.

For Claude Code, run `claude plugin marketplace update bazutte-plugins`, followed by `claude plugin update bazutte@bazutte-plugins`. For Codex, run `codex plugin marketplace upgrade bazutte-plugins`. Start a new conversation after updating.

## Release status

Version `0.4.0` renames the research skill from `youtube-research` to `bazutte-research` and clarifies the provider, data sources, custom metrics, terms, and data sharing with AI clients. Update any invocations that use the old name. Guidance for preserving every returned field, thumbnails, spreading rate, and hit score remains available. Once it reaches the distribution repository's `main` branch, use the update commands above to get it. The server and plugin are updated separately; server-generated reports are used only when the connected server supports them.

See [CHANGELOG.md](CHANGELOG.md) for release notes. The distribution repository provides user-facing files on `main` and version tags.

## References

- [Codex plugin packaging and distribution](https://developers.openai.com/plugins/build/plugins)
- [Claude plugin installation](https://claude.com/docs/plugins/overview)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code marketplace hosting and updates](https://code.claude.com/docs/en/plugins/host-marketplace)
