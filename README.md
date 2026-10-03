# Bazutte Plugins

[日本語](README.md) | [English](README.en.md)

Claude CodeとCodexを、MCP経由で[Bazutte](https://bazutte.com)へ接続するプラグインです。このリポジトリでは、マーケットのカタログとクライアント別の接続定義を配布します。

## 必要な環境

- Gitと、Claude CodeまたはCodex CLI。
- MCPサービスを利用できるBazutteアカウント。
- GitHubと`https://bazutte.com/mcp`へのネットワーク接続。

接続先はBazutteの本番MCPです。インストールや有効化によって、接続や認証の案内が始まる場合があります。

## 導入手順

### Codex

```bash
codex plugin marketplace add https://github.com/bazutte/bazutte-plugins.git --ref main
codex plugin add bazutte@bazutte-plugins
codex mcp login bazutte
```

3行目でBazutteのOAuth認証を開始します。ブラウザでログインと接続の許可を完了し、新しいCodexセッションを開いてください。Codex CLIでのサーバー名は`bazutte`です。

### Claude Code

```bash
claude plugin marketplace add https://github.com/bazutte/bazutte-plugins.git#main
claude plugin install bazutte@bazutte-plugins
claude mcp login plugin:bazutte:bazutte
```

3行目は対話できる端末で実行してください。プラグインのサーバー`plugin:bazutte:bazutte`のOAuth認証を開始します。ブラウザでログインと接続の許可を完了し、新しいClaude Codeセッションを開いてください。セッション内の`/mcp`からも認証できます。

## 接続確認

認証後、AIへ次のメッセージを送ってください。

```text
Bazutteのpingを実行して、接続できているか確認してください。
```

ツールから`pong from bazutte`が返れば、接続を確認できます。

## 認証とプライバシー

利用者自身がBazutteへログインし、OAuthで接続を許可します。配布物には、共有APIキー・アクセストークン・個人情報・アカウントのデータを含めません。接続定義を公開しても、Bazutteのデータ利用権が付与されることはありません。

配布物はプラグイン定義と接続設定で構成します。インストール用スクリプトやライフサイクルhooksはなく、クライアントとGit以外の実行環境を追加する必要もありません。

## 対応クライアント

| クライアント | プラグイン定義 | MCP設定 | 認証 |
| --- | --- | --- | --- |
| Codex CLI | `plugins/bazutte/plugin.json` | `mcp.json`（`streamable-http`） | Bazutte OAuth |
| Claude Code | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json`（`http`） | Bazutte OAuth |

接続定義はCodex CLI `0.160.0`とClaude Code `2.1.284`で確認しています。確認した版であり、最低対応版を保証するものではありません。

## トラブル対応

| 症状 | 確認すること |
| --- | --- |
| Gitの配布元を取得できない | Gitが導入済みか、GitHubへ接続できるかを確認します。配布元に`main`ブランチとカタログがあることも確認してください。 |
| プラグインが表示されない・有効にならない | マーケット名が`bazutte-plugins`、プラグイン名が`bazutte@bazutte-plugins`かを確認します。インストール済みプラグインの状態を確認し、新しいセッションを開いてください。 |
| 認証に失敗する・ツールが使えない | MCP設定から、同梱サーバーの認証状態とBazutteアカウントの利用権限を確認してください。 |

問い合わせは[Bazutteの公開窓口](https://bazutte.com)をご利用ください。クライアントの版と、秘密情報を除いたエラーメッセージを添えてください。

## ファイル構成

```text
.agents/plugins/marketplace.json         # Codex catalog / Codex用カタログ
.claude-plugin/marketplace.json          # Claude Code catalog / Claude Code用カタログ
plugins/bazutte/
  plugin.json                           # Portable manifest / 共通形式の定義
  mcp.json                              # Codex MCP settings / Codex用MCP設定
  .claude-plugin/plugin.json             # Claude Code manifest / Claude Code用の定義
  .mcp.json                             # Claude Code MCP settings / Claude Code用MCP設定
```

両方のカタログで、プラグイン名は`bazutte@bazutte-plugins`です。クライアント別のMCP設定は、同じ本番エンドポイントを指します。

## 更新

クライアントのマーケット・プラグイン更新操作で、新しいリリースを取得してください。Claude Codeの自社マーケットは自動更新が既定で無効です。必要に応じてマーケット設定から有効にできます。

## リリース状況

`0.1.1`の配布を準備しています。配布開始後、上記の手順で導入し、OAuth認証と`ping`の応答を確認してください。

リリースごとの変更は[CHANGELOG.md](CHANGELOG.md)に記載します。配布元の`main`に利用者向けファイルと版タグを置きます。

## 参考資料

- [Codexのプラグイン作成と配布](https://developers.openai.com/plugins/build/plugins)
- [Claude Codeのマーケット作成](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Codeの配布と更新](https://code.claude.com/docs/en/plugins/host-marketplace)
