# Bazutte

YouTube research, done with a single question to Claude. Claude answers with real view and subscriber counts from Bazutte's Japanese YouTube data, updated every day.

## Ask Claude to

- Find ideas that worked for channels your size
- See whether a video beat its channel's usual views, and by how much
- Ride trends early with keywords that are starting to rise
- Discover fast-growing competitors and sponsorship candidates
- Check a channel's name changes and ban history before you reach out

For example: "Use Bazutte to find videos that beat their channel's usual views this week among channels like mine."

## Install

Just sign in with your Bazutte account to connect. In Claude Code, run:

```text
/plugin install bazutte --marketplace bazutte/bazutte-plugins
```

Then sign in to Bazutte when prompted. For Claude on the web, Codex, and ChatGPT, follow the setup guide at https://info.bazutte.com/en/mcp.

## What it runs and sends

The plugin connects to the Bazutte MCP server and adds a research skill. All tools are read-only. They query only Bazutte's own database and never change anything in Bazutte or on YouTube.

When you ask a question, your AI client sends the tool arguments it chooses (for example a keyword, a channel URL, or a date range) to `https://bazutte.com/mcp`. Bazutte uses OAuth to sign you in and records each call to count usage. The plugin does not read your files and does not send your conversation to Bazutte.

This is not an official YouTube plugin. YouTube is a trademark of Google LLC.

## Links

- Setup guide: https://info.bazutte.com/en/mcp
- Support: https://forms.gle/L9ZQ757jkqdDA4dJ8
- Privacy policy: https://info.bazutte.com/en/privacy
- Terms of service: https://info.bazutte.com/en/terms

## 日本語

YouTubeリサーチが、Claudeへの質問ひとつで終わります。Bazutteが毎日更新している日本のYouTubeのデータをもとに、Claudeが実際の再生数と登録者数で答えます。

- 近い規模のチャンネルで当たった企画を探す
- 自分や競合の動画が、いつもの何倍見られたかを確かめる
- 伸び始めたキーワードで、流行に早く乗る
- 伸びている新しい競合や、タイアップ先の候補を探す
- チャンネル名の変更やBANの履歴を、依頼の前に確認する

接続はBazutteのアカウントでログインするだけです。Claude Code では `/plugin install bazutte --marketplace bazutte/bazutte-plugins` で入れ、案内に従ってログインします。

ツールはすべて読み取り専用で、Bazutte のデータベースだけを読みます。質問すると、AI が選んだツールの引数（キーワード、チャンネルの URL、期間など）が `https://bazutte.com/mcp` へ送られます。ログインは OAuth で行い、利用枠を数えるために呼び出しを記録します。ファイルや会話の内容は Bazutte へ送りません。

- 使い方: https://info.bazutte.com/mcp
- お問い合わせ: https://forms.gle/L9ZQ757jkqdDA4dJ8
- プライバシーポリシー: https://info.bazutte.com/privacy
- 利用規約: https://info.bazutte.com/terms
