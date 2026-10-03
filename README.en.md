# Bazutte Plugins

[日本語](README.md) | [English](README.en.md)

Connect Claude Code and Codex to [Bazutte](https://bazutte.com) through MCP. This repository provides a plugin marketplace and client-specific connection definitions.

## Requirements

- Git and either Claude Code or Codex CLI.
- A Bazutte account with permission to use the MCP service.
- Network access to GitHub and `https://bazutte.com/mcp`.

The plugin connects to Bazutte's production MCP endpoint. Installing or enabling it may initiate a connection or an authentication prompt.

## Quick start

### Codex

```bash
codex plugin marketplace add https://github.com/bazutte/bazutte-plugins.git --ref main
codex plugin add bazutte@bazutte-plugins
codex mcp login bazutte
```

The third command starts Bazutte OAuth authentication. Complete sign-in and consent in your browser, then start a new Codex session. The installed server is named `bazutte` in Codex CLI.

### Claude Code

```bash
claude plugin marketplace add https://github.com/bazutte/bazutte-plugins.git#main
claude plugin install bazutte@bazutte-plugins
claude mcp login plugin:bazutte:bazutte
```

Run the third command in an interactive terminal. It starts OAuth authentication for the plugin-scoped server `plugin:bazutte:bazutte`. Complete sign-in and consent in your browser, then start a new Claude Code session. You can also authenticate this server from `/mcp` in a session.

## Verify the connection

After authentication, ask your assistant:

```text
Run Bazutte's ping tool and check whether the connection is working.
```

A tool response of `pong from bazutte` confirms the connection.

## Authentication and privacy

Each user signs in to Bazutte and grants access through OAuth. No shared API key, access token, personal information, or account data is included in the package. Publishing the connection definition does not grant access to Bazutte data.

The package contains manifests and connection settings. It has no installation scripts, lifecycle hooks, or additional runtime dependencies beyond the client and Git.

## Compatibility

| Client | Plugin manifest | MCP definition | Authentication |
| --- | --- | --- | --- |
| Codex CLI | `plugins/bazutte/plugin.json` | `mcp.json` (`streamable-http`) | Bazutte OAuth |
| Claude Code | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json` (`http`) | Bazutte OAuth |

The connection definitions were checked with Codex CLI `0.160.0` and Claude Code `2.1.284`. These are tested versions, not minimum-version guarantees.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| The Git source cannot be fetched | Confirm Git is installed and GitHub is reachable. Confirm the repository has the `main` branch and the marketplace catalog. |
| The plugin is not listed or enabled | Confirm the marketplace is named `bazutte-plugins` and the plugin ID is `bazutte@bazutte-plugins`. Check the client's installed plugins, then open a new session. |
| Authentication fails or the tool is unavailable | Check the bundled server's authentication state and your Bazutte account's permissions in the client's MCP settings. |

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
```

Both catalogs expose `bazutte@bazutte-plugins`. Client-specific MCP settings point to the same production endpoint.

## Updates

Use your client's marketplace and plugin update commands to fetch a new release. Automatic updates for custom Claude Code marketplaces are off by default; users can enable them in the marketplace settings.

## Release status

Version `0.1.1` is being prepared for distribution. After distribution starts, follow the installation steps above and verify OAuth authentication and the `ping` response.

See [CHANGELOG.md](CHANGELOG.md) for release notes. The distribution repository provides user-facing files on `main` and version tags.

## References

- [Codex plugin packaging and distribution](https://developers.openai.com/plugins/build/plugins)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code marketplace hosting and updates](https://code.claude.com/docs/en/plugins/host-marketplace)
