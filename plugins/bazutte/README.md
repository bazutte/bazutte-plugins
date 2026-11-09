# Bazutte

Research YouTube videos and channels with Bazutte's stored data from Claude, Claude Code, and Codex. The plugin connects to the Bazutte MCP server and adds a research skill for finding videos that are growing, comparing competitor channels, and checking channel history.

## Install

In Claude Code, run:

```text
/plugin install bazutte --marketplace bazutte/bazutte-plugins
```

Then sign in to Bazutte when prompted. For Claude on the web, Codex, and ChatGPT, follow the setup guide at https://info.bazutte.com/mcp.

## What it does

- Finds videos and channels in Bazutte's saved data, including rankings, recent uploads, and videos that perform above a channel's usual level.
- Compares channels and finds similar or related channels.
- Shows keyword trends, channel name changes, and recorded ban and restore history.

All tools are read-only. They query only Bazutte's own database and never change anything in Bazutte or on YouTube. This is not an official YouTube plugin. YouTube is a trademark of Google LLC.

## Data it sends

When you ask a question, your AI client sends the tool arguments it chooses (for example a keyword, a channel URL, or a date range) to `https://bazutte.com/mcp`. Bazutte uses OAuth to sign you in and records each call to count usage. The plugin does not read your files and does not send your conversation to Bazutte.

## Requirements and links

- A Bazutte account that can use the MCP service: https://bazutte.com
- Setup guide: https://info.bazutte.com/mcp
- Support: https://forms.gle/L9ZQ757jkqdDA4dJ8
- Privacy policy: https://info.bazutte.com/en/privacy
- Terms of service: https://info.bazutte.com/en/terms

## 日本語

Bazutte が保存したデータを使い、Claude・Claude Code・Codex から YouTube の動画とチャンネルを調べるプラグインです。Bazutte の MCP サーバーへの接続と、伸びている動画の発見・競合チャンネルの比較・チャンネルの履歴確認のための調査スキルを含みます。

ツールはすべて読み取り専用で、Bazutte のデータベースだけを読みます。Bazutte と YouTube のデータは変更しません。

Claude Code では `/plugin install bazutte --marketplace bazutte/bazutte-plugins` で入れ、案内に従って Bazutte にログインします。

質問すると、AI が選んだツールの引数（キーワード、チャンネルの URL、期間など）が `https://bazutte.com/mcp` へ送られます。ログインは OAuth で行い、利用枠を数えるために呼び出しを記録します。ファイルや会話の内容は Bazutte へ送りません。

- 使い方: https://info.bazutte.com/mcp
- お問い合わせ: https://forms.gle/L9ZQ757jkqdDA4dJ8
- プライバシーポリシー: https://info.bazutte.com/privacy
- 利用規約: https://info.bazutte.com/terms
