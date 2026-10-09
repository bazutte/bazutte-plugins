# Bazutte Plugins

[日本語](README.md) | [English](README.en.md)

Claude・Claude Code・Codexから、[Bazutte](https://bazutte.com)の保存データでYouTubeの動画・チャンネルを調べる、Bazutte提供のプラグインです。MCPの接続設定と、動画の発見・競合比較・チャンネル分析を助ける調査skillをまとめて導入できます。

データの収集元にはYouTube API Servicesが含まれます。MCPは保存された情報とBazutte独自指標をBazutteの形式で返します。YouTubeの公式プラグインではなく、YouTube Data APIを直接呼び出す汎用クライアントでもありません。YouTubeはGoogle LLCの商標です。

## 必要な環境

- Claudeの有料プラン（Pro・Max・Team・Enterprise）、またはClaude Code・Codex CLI。
- CLIで導入する場合はGit。
- MCPサービスを利用できるBazutteアカウント。
- GitHubと`https://bazutte.com/mcp`へのネットワーク接続。

接続先はBazutteの本番MCPです。インストールや有効化によって、接続や認証の案内が始まる場合があります。

## 導入手順

Bazutteプラグインは各AIの公式ディレクトリにはまだ掲載していません。GitHubの`bazutte/bazutte-plugins`をマーケットとして追加し、そこからBazutteを導入してください。

### Claude（ブラウザ・通常アプリ）

1. [Claudeのプラグイン画面](https://claude.ai/customize/plugins)で「Add → Add marketplace」を選びます。
2. `https://github.com/bazutte/bazutte-plugins`を入力し、マーケットを追加します。表示された「Bazutte」を追加してください。
3. プラグインの「Connectors」を開きます。Bazutteが未追加なら「Add」で追加し、「Connect」で接続してください。Bazutteにログインして接続を許可します。

CLIのインストールやMCP URLの手入力は不要です。追加したプラグインは、同じアカウントでログインしたClaudeのアプリとClaude Codeにも同期されます。Team・Enterpriseでは、管理者が先にBazutteのコネクタを追加してください。無料プラン・プラグインメニューがない場合は、[Bazutteの「AIと連携」](https://bazutte.com/ai_integration)でClaudeを選び、補足にある手動設定を利用できます。

Codex・Claude Codeは、同じPCに各AIのCLIを先にインストールしてください。以下のコマンドをターミナルで実行し、最後の行で開くブラウザでBazutteにログインします。アプリとCLIの手順は共通です。

### Codex（アプリ・CLI・エディタ拡張）

```bash
codex plugin marketplace add bazutte/bazutte-plugins
codex plugin add bazutte@bazutte-plugins
codex mcp login bazutte
```

3行目でBazutteのOAuth認証を開始します。ブラウザで接続を許可し、Codexのアプリ・CLI・エディタ拡張を開き直して新しい会話を始めてください。サーバー名は`bazutte`です。

### Claude Code（アプリ・CLI）

```bash
claude plugin install bazutte --marketplace bazutte/bazutte-plugins
claude mcp login plugin:bazutte:bazutte
```

1行目でマーケットの追加とプラグインの導入をまとめて行います。エラーになる場合は`claude update`でClaude Codeを最新にしてください。2行目は対話できる端末で実行し、ブラウザで接続を許可して、Claude Codeを開き直して新しい会話を始めます。アプリではローカルセッションを使ってください。認証コマンドが使えない場合は、会話で`/mcp`を開き、`plugin:bazutte:bazutte`の「Authenticate」から認証できます。

ChatGPTの画面からはGitHubのマーケットを追加できないため、接続先URLを登録して使います。手順は[Bazutteの「AIと連携」](https://bazutte.com/ai_integration)を確認してください。調査skillも使う場合は、上記のCodexの手順でプラグインを導入してください。

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

```text
Bazutteで昨日公開された動画の再生数上位100件を、登録者3,000人以下で調べて。サムネイル・拡散率・ヒットスコアを表示し、取得した全項目を資料に残して。
```

同梱の`bazutte-research`は、質問の目的に合うデータと比較指標を選び、出所と動画・チャンネルのYouTubeリンクを添えて結果を示します。企画案を依頼した場合は、確認できた傾向と提案の仮説を分けます。保存データの更新日時と取得日時は区別し、リアルタイムの値を保証しません。

自然文で依頼するだけで使えます。必要ならClaude Codeでは`/bazutte:bazutte-research`、Codexでは`$bazutte-research`で指定してください。

## 調べられることと資料保存

動画ランキング、チャンネルの比較・詳細、過去の投稿、動画の指標履歴、キーワードランキング、チャンネル名の変更、BAN・復旧の履歴を調べられます。「Bazutteで何ができる？」と尋ねると、接続中のツールの説明に基づく質問例を案内します。期間・取得上限・利用権限はツールごとに異なります。

「全項目を資料に」と依頼した場合は、列を絞らず、取得した行・項目と条件・警告を資料に残す手順を使います。対応サーバーではHTML資料を取得して保存し、未対応の場合は取得済みのデータから作成します。サーバーのHTML資料は一時的なもので、読み取り・ファイル保存の可否はAIクライアントにも依存します。全項目は取得した範囲を指し、Bazutte内の全データを意味しません。

返されたサムネイルは外部URLで表示し、元の動画へのリンクを残します。表示できない場合は画像リンクを示します。拡散率・バズスコア・ヒットスコアはBazutte独自の倍率指標で、YouTube公式の指標や評価ではありません。ヒットスコアの`1.0`には算出不能時の代替値も含まれます。

資料は取得時点の情報です。保存・オフライン画像の埋め込み・再配布には、適用される利用条件と更新・削除の要件に従ってください。保存によって無期限の保管権や再配布権が付与されることはありません。サーバーの資料の有効期限は、一時資料にアクセスできる期限であり、データの利用許諾期限ではありません。

## 認証とプライバシー

利用者自身がBazutteへログインし、OAuthで接続を許可します。配布物には、共有APIキー・アクセストークン・個人情報・アカウントのデータを含めません。接続定義を公開しても、Bazutteのデータ利用権が付与されることはありません。

利用前に[Bazutte利用規約](https://info.bazutte.com/terms)と[プライバシーポリシー](https://info.bazutte.com/privacy)を確認し、同意してください。本サービスの利用には[YouTube利用規約](https://www.youtube.com/t/terms)も適用され、利用者はこれに同意する必要があります。Googleのデータの取り扱いは[Googleプライバシーポリシー](https://policies.google.com/privacy)を参照してください。

ツールに渡す検索条件や識別子はBazutteへ送信され、取得結果（動画・チャンネル情報、指標、資料など）は利用中のAIクライアントへ渡ります。AI側での保存・共有・モデル改善への利用は、そのサービスの設定と規約・プライバシーポリシーも確認してください。Bazutteへの接続許可は、YouTubeアカウントの操作や非公開アナリティクスの取得を許可するものではありません。

接続をやめる場合は、利用中のAIクライアントのMCP・Connectors設定からBazutteを切断・解除してください。接続解除だけでAI側の会話や保存済み資料が消えるとは限りません。AI側の履歴や保存ファイルは、そのサービスの削除手順で扱ってください。Bazutteに関するデータの問い合わせ・削除依頼は、プライバシーポリシー記載の窓口へ連絡してください。

配布物はプラグイン定義、接続設定、自然言語で書いたskillで構成します。インストール用スクリプトやライフサイクルhooksはありません。Claudeの画面から追加する場合は、GitをPCへインストールする必要もありません。

## 対応クライアント

| クライアント | プラグイン定義 | MCP設定 | 認証 |
| --- | --- | --- | --- |
| Claude（有料プラン） | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json`（`http`） | プラグインのConnectorsからBazutte OAuth |
| Codex CLI | `plugins/bazutte/plugin.json` | `mcp.json`（`streamable-http`） | Bazutte OAuth |
| Claude Code | `plugins/bazutte/.claude-plugin/plugin.json` | `.mcp.json`（`http`） | Bazutte OAuth |

導入コマンドはCodex CLI `0.162.0`とClaude Code `2.1.295`で確認しています。確認した版であり、最低対応版を保証するものではありません。Claudeの画面からの追加は公式仕様に基づく手順で、実アカウントでの接続は未検証です。

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
  skills/bazutte-research/SKILL.md        # Bazutte research / 動画・チャンネル調査
```

両方のカタログで、プラグイン名は`bazutte@bazutte-plugins`です。クライアント別のMCP設定は、同じ本番エンドポイントを指します。

## 更新

クライアントのマーケット・プラグイン更新操作で、新しいリリースを取得してください。Claudeの画面から追加したマーケットは「Check for updates」で更新できます。GitHubのマーケットでは「Sync automatically」を有効にすることもできます。Claude Codeの自社マーケットは自動更新が既定で無効です。必要に応じてマーケット設定から有効にできます。

Claude Codeでは`claude plugin marketplace update bazutte-plugins`、続けて`claude plugin update bazutte@bazutte-plugins`を実行します。Codexでは`codex plugin marketplace upgrade bazutte-plugins`を実行します。更新後は新しい会話を開いてください。

## リリース状況

`0.4.0`では調査skillを`youtube-research`から`bazutte-research`へ改名し、提供元・データの出所・独自指標・利用条件とAIへのデータ共有の説明を整えています。旧名で呼び出していた場合は、新しい名前に変更してください。全項目・サムネイル・拡散率・ヒットスコアを残す手順は継続します。配布元の`main`に反映された後、上記の更新手順で取得できます。サーバーとプラグインは別に更新されるため、資料機能は接続中のサーバーが対応している場合に使います。

リリースごとの変更は[CHANGELOG.md](CHANGELOG.md)に記載します。配布元の`main`に利用者向けファイルと版タグを置きます。

## 参考資料

- [Codexのプラグイン作成と配布](https://developers.openai.com/plugins/build/plugins)
- [Claudeのプラグイン導入](https://claude.com/docs/plugins/overview)
- [Claude Codeのマーケット作成](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Codeの配布と更新](https://code.claude.com/docs/en/plugins/host-marketplace)
