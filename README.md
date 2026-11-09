# Bazutte Plugins

[English](README.md) | [日本語](README.ja.md)

Research the Japanese YouTube market just by asking your AI. Answers use real view and subscriber counts from [Bazutte](https://bazutte.com)'s Japanese YouTube data, updated every day. This plugin connects Claude, Claude Code, and Codex to the Bazutte MCP server (`https://bazutte.com/mcp`) and adds a research skill.

## Set up

Send this one line to an AI that can add MCP servers by itself (Codex, Claude Code, and others):

```text
Read https://info.bazutte.com/mcp and set up Bazutte
```

Then sign in to Bazutte in the browser window that opens.

**Claude** (paid plan): In **Customize → Plugins**, choose **Add marketplace**, enter `https://github.com/bazutte/bazutte-plugins`, and add **Bazutte**. Then open **Connectors** and choose **Connect**. On Team and Enterprise, an owner adds the connector first.

**ChatGPT**: Add a custom MCP server with the URL `https://bazutte.com/mcp` and OAuth.

Step-by-step guides for each AI: [info.bazutte.com/en/mcp](https://info.bazutte.com/en/mcp).

<details>
<summary>Install with commands</summary>

```bash
# Codex
codex plugin marketplace add bazutte/bazutte-plugins
codex plugin add bazutte@bazutte-plugins
codex mcp login bazutte

# Claude Code
claude plugin marketplace add bazutte/bazutte-plugins
claude plugin install bazutte@bazutte-plugins
claude mcp login plugin:bazutte:bazutte
```

To update, run `codex plugin marketplace upgrade bazutte-plugins`, or `claude plugin marketplace update bazutte-plugins` and `claude plugin update bazutte@bazutte-plugins`. Then start a new conversation.

</details>

## What you can ask

```text
Use Bazutte to find the 10 most viewed videos published yesterday.
Use Bazutte to compare this channel with its competitors over the last 30 days.
```

You can research video rankings, growing videos, competitor and similar channels, recent uploads, keyword trends, channel name changes, and ban history. All tools are read-only.

## Authentication and data

Each user signs in to Bazutte with OAuth. The package contains no API keys or account data. Tool arguments (such as keywords and channel URLs) are sent to Bazutte, and results are passed to your AI client. See the [Privacy Policy](https://info.bazutte.com/en/privacy) and [Terms of Service](https://info.bazutte.com/en/terms).

Data sources include YouTube API Services, so the [YouTube Terms of Service](https://www.youtube.com/t/terms) and [Google Privacy Policy](https://policies.google.com/privacy) also apply. This is not an official YouTube plugin. YouTube is a trademark of Google LLC.

## Support

[Contact form](https://forms.gle/L9ZQ757jkqdDA4dJ8) · [Release notes](CHANGELOG.md)

## License

[Apache License 2.0](LICENSE). It grants no rights to the Bazutte name or logo. Use of the Bazutte service is governed by the [Terms of Service](https://info.bazutte.com/en/terms).
