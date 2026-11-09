# Bazutte Plugins

[English](README.md) | [日本語](README.ja.md)

[Bazutte](https://bazutte.com)のデータで、AIからYouTubeの動画とチャンネルを調べるプラグインです。Claude・Claude Code・CodexをBazutteのMCPサーバー（`https://bazutte.com/mcp`）へつなぎ、調査用のskillを加えます。

## 導入

MCPを自分で追加できるAI（Codex・Claude Codeなど）に、次の1行を送ります。

```text
https://info.bazutte.com/mcp を読んで、Bazutteを導入して
```

開いたブラウザでBazutteにログインすれば完了です。

**Claude**（有料プラン）: **カスタマイズ → プラグイン**で**マーケットプレイスを追加**を選び、`https://github.com/bazutte/bazutte-plugins`を入力して**Bazutte**を追加します。続けて**コネクタ**で**接続**を選びます。Team・Enterpriseでは先にオーナーがコネクタを追加します。

**ChatGPT**: カスタムMCPサーバーとして、URL `https://bazutte.com/mcp`・認証OAuthで追加します。

AIごとの詳しい手順: [info.bazutte.com/mcp](https://info.bazutte.com/mcp)

<details>
<summary>コマンドで導入する</summary>

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

更新は`codex plugin marketplace upgrade bazutte-plugins`、またはClaude Codeでは`claude plugin marketplace update bazutte-plugins`と`claude plugin update bazutte@bazutte-plugins`を実行し、新しい会話を始めます。

</details>

## 質問の例

```text
Bazutteで昨日公開された動画を再生数の多い順に10本探して
Bazutteでこのチャンネルを直近30日で競合と比べて
```

動画ランキング、伸びている動画、競合・類似チャンネル、直近の投稿、キーワードの流行、チャンネル名の変更、BANの履歴を調べられます。ツールはすべて読み取り専用です。

## 認証とデータ

利用者ごとにOAuthでBazutteへログインします。配布物にAPIキーやアカウントのデータは含みません。ツールの引数（キーワード・チャンネルのURLなど）はBazutteへ送られ、結果は利用中のAIクライアントへ渡ります。[プライバシーポリシー](https://info.bazutte.com/privacy)と[利用規約](https://info.bazutte.com/terms)を確認してください。

データの収集元にYouTube API Servicesを含むため、[YouTube利用規約](https://www.youtube.com/t/terms)と[Googleプライバシーポリシー](https://policies.google.com/privacy)も適用されます。YouTubeの公式プラグインではありません。YouTubeはGoogle LLCの商標です。

## サポート

[お問い合わせフォーム](https://forms.gle/L9ZQ757jkqdDA4dJ8) · [更新履歴（英語）](CHANGELOG.md)

## ライセンス

[Apache License 2.0](LICENSE)。Bazutteの名前とロゴを使う権利は含みません。Bazutteのサービスの利用には[利用規約](https://info.bazutte.com/terms)が適用されます。
