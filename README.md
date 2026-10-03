# Bazutte Plugins

[日本語](README.md) | [English](README.en.md)

Claude・Claude Code・Codexから、[Bazutte](https://bazutte.com)のYouTubeデータを調べるプラグインです。MCPの接続設定と、動画の発見・競合比較・チャンネル分析を助ける調査skillをまとめて導入できます。

## 必要な環境

- Claudeの有料プラン（Pro・Max・Team・Enterprise）、またはClaude Code・Codex CLI。
- CLIで導入する場合はGit。
- MCPサービスを利用できるBazutteアカウント。
- GitHubと`https://bazutte.com/mcp`へのネットワーク接続。

接続先はBazutteの本番MCPです。インストールや有効化によって、接続や認証の案内が始まる場合があります。

## 導入手順

### Claude（ブラウザ・通常アプリ）

1. [Claudeのプラグイン画面](https://claude.ai/customize/plugins)で「Add → Add marketplace」を選びます。
2. `https://github.com/bazutte/bazutte-plugins`を入力し、マーケットを追加します。表示された「Bazutte」を追加してください。
3. プラグインの「Connectors」を開きます。Bazutteが未追加なら「Add」で追加し、「Connect」で接続してください。Bazutteにログインして接続を許可します。

CLIのインストールやMCP URLの手入力は不要です。Team・Enterpriseでは、管理者が先にBazutteのコネクタを追加してください。無料プラン・プラグインメニューがない場合は、[Bazutteの「AIと連携」](https://bazutte.com/ai_integration)でClaudeを選び、補足にある手動設定を利用できます。

Codex・Claude Codeは、同じPCに各AIのCLIを先にインストールしてください。以下の3行をターミナルで実行し、ブラウザでBazutteにログインします。アプリとCLIの手順は共通です。

### Codex（アプリ・CLI・エディタ拡張）

```bash
codex plugin marketplace add https://github.com/bazutte/bazutte-plugins.git --ref main
codex plugin add bazutte@bazutte-plugins
codex mcp login bazutte
```

3行目でBazutteのOAuth認証を開始します。ブラウザで接続を許可し、Codexのアプリ・CLI・エディタ拡張を開き直して新しい会話を始めてください。サーバー名は`bazutte`です。

### Claude Code（アプリ・CLI）

```bash
claude plugin marketplace add https://github.com/bazutte/bazutte-plugins.git#main
claude plugin install bazutte@bazutte-plugins
claude mcp login plugin:bazutte:bazutte
```

3行目は対話できる端末で実行してください。ブラウザで接続を許可し、Claude Codeを開き直して新しい会話を始めます。アプリではローカルセッションを使ってください。認証コマンドが使えない場合は、会話で`/mcp`を開き、`plugin:bazutte:bazutte`の「Authenticate」から認証できます。

ChatGPTをお使いの場合は、[Bazutteの「AIと連携」](https://bazutte.com/ai_integration)でコネクタの導入手順を確認してください。

## そのまま質問する

接続後は、ツール名を覚えずに質問できます。

```text
Bazutteで昨日公開された動画の再生数上位10件を、動画とチャンネルのリンク付きで教えて。
```

```text
Bazutteで登録者3,000人以下のチャンネルから伸びている動画を探して。
```

```text
このYouTubeチャンネルをBazutteで調べて、最近30日の再生数増加と投稿数を競合と比較して。
```

同梱の`youtube-research`は、質問の目的に合うデータと比較指標を選び、動画・チャンネルのリンクを添えて結果を示します。企画案を依頼した場合は、確認できた傾向と提案の仮説を分けます。分析にはBazutteの保存データを使います。

自然文で依頼するだけで使えます。必要ならClaude Codeでは`/bazutte:youtube-research`、Codexでは`$youtube-research`で指定してください。

## 認証とプライバシー

利用者自身がBazutteへログインし、OAuthで接続を許可します。配布物には、共有APIキー・アクセストークン・個人情報・アカウントのデータを含めません。接続定義を公開しても、Bazutteのデータ利用権が付与されることはありません。

配布物はプラグイン定義、接続設定、自然言語で書いたskillで構成します。インストール用スクリプトやライフサイクルhooksはありません。Claudeの画面から追加する場合は、GitをPCへインストールする必要もありません。

## 対応クライアント

| クライアント | プラグイン定義 | MCP設定 | 認証 |
| --- | --- | --- | --- |
| Claude（有料プラン） | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json`（`http`） | プラグインのConnectorsからBazutte OAuth |
| Codex CLI | `plugins/bazutte/plugin.json` | `mcp.json`（`streamable-http`） | Bazutte OAuth |
| Claude Code | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json`（`http`） | Bazutte OAuth |

接続定義はCodex CLI `0.160.0`とClaude Code `2.1.284`で確認しています。確認した版であり、最低対応版を保証するものではありません。Claudeの画面からの追加は公式仕様に基づく手順で、実アカウントでの接続は未検証です。

## トラブル対応

| 症状 | 確認すること |
| --- | --- |
| Gitの配布元を取得できない | GitHubへ接続できるか、配布元に`main`ブランチとカタログがあるかを確認します。CLIで導入する場合はGitも必要です。 |
| プラグインが表示されない・有効にならない | マーケット名が`bazutte-plugins`、プラグイン名が`bazutte@bazutte-plugins`かを確認します。インストール済みプラグインの状態を確認し、新しいセッションを開いてください。 |
| 認証に失敗する・ツールが使えない | MCP設定から、同梱サーバーの認証状態とBazutteアカウントの利用権限を確認してください。 |
| 以前の手動設定と重複する | 以前の接続先を`codex mcp get bazutte`または`claude mcp get bazutte`で確認します。手動設定を使わない場合は、`codex mcp remove bazutte`または`claude mcp remove --scope user bazutte`で削除してからプラグインを導入してください。 |
| 週間利用枠を超えた | 「Bazutteの今週の利用枠を教えて」と質問し、返されたリセット日時を確認してください。 |

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
  skills/youtube-research/SKILL.md       # YouTube research / 動画・チャンネル調査
```

両方のカタログで、プラグイン名は`bazutte@bazutte-plugins`です。クライアント別のMCP設定は、同じ本番エンドポイントを指します。

## 更新

クライアントのマーケット・プラグイン更新操作で、新しいリリースを取得してください。Claudeの画面から追加したマーケットは「Check for updates」で更新できます。GitHubのマーケットでは「Sync automatically」を有効にすることもできます。Claude Codeの自社マーケットは自動更新が既定で無効です。必要に応じてマーケット設定から有効にできます。

Claude Codeでは`claude plugin marketplace update bazutte-plugins`、続けて`claude plugin update bazutte@bazutte-plugins`を実行します。Codexでは`codex plugin marketplace upgrade bazutte-plugins`を実行します。更新後は新しい会話を開いてください。

## リリース状況

`0.2.0`ではYouTube調査skillを追加しています。配布元の`main`に反映された後、上記の更新手順で取得できます。

リリースごとの変更は[CHANGELOG.md](CHANGELOG.md)に記載します。配布元の`main`に利用者向けファイルと版タグを置きます。

## 参考資料

- [Codexのプラグイン作成と配布](https://developers.openai.com/plugins/build/plugins)
- [Claudeのプラグイン導入](https://claude.com/docs/plugins/overview)
- [Claude Codeのマーケット作成](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Codeの配布と更新](https://code.claude.com/docs/en/plugins/host-marketplace)
