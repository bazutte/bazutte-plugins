# 更新履歴 / Changelog

## 0.4.1 — 2026-10-13

- 応答が大きすぎるエラーでは同じ呼び出しを繰り返さず、チャンネル詳細のキーワード順位と関連チャンネルの項目を絞って1回だけ再試行する手順を追加。 / Add guidance to retry once with narrowed keyword rank and related-channel fields instead of repeating the same call after a response-too-large error.
- 全項目の取得を1ページ50件以下に分け、AIクライアントが大きな結果をファイルへ退避した場合はそのファイルから資料を保存する手順を追加。 / Retrieve full-field pages of 50 or fewer and save reports from the file when the AI client offloads a large result.
- 資料の既定の保存先を作業ディレクトリ直下の`bazutte-reports/`に設定。 / Set the default report location to `bazutte-reports/` in the working directory.

## 0.4.0 — 2026-10-05

- 調査skillを`bazutte-research`へ改名。旧名の呼び出しは新しい名前へ変更してください。 / Rename the research skill to `bazutte-research`; update invocations using the previous name.
- Bazutteの提供主体、YouTube由来の情報と独自指標の区別、データの時点を明記。 / Clarify Bazutte as the provider, distinguish YouTube-sourced information from custom metrics, and preserve data timestamps.
- 利用条件・プライバシーへのリンク、AIクライアントへのデータ共有、接続解除、保存・再配布の説明を追加。 / Add terms and privacy links and explain AI-client data sharing, disconnection, retention, and redistribution.

## 0.3.0 — 2026-10-05

- 全取得項目を残す資料の取得・保存と、未対応サーバーでの代替手順を追加。 / Add report retrieval and saving instructions that preserve every returned field, with a fallback for servers without report support.
- サムネイル・拡散率・ヒットスコアの表示、画像の外部参照と埋め込みの区別、ページをまたぐ件数確認を明記。 / Explain thumbnails and score metrics, distinguish linked images from embedded files, and verify counts across pages.
- キーワード、名称変更、BAN・復旧の履歴の調査と、利用可能なツールに基づく使い方の案内を追加。 / Cover keyword rankings, name changes, stored ban and reinstatement history, and capability guidance based on available tools.

## 0.2.0 — 2026-10-04

- 動画の発見・競合比較・チャンネル分析から企画の根拠まで調べる`youtube-research`を同梱。 / Bundle `youtube-research` for video discovery, competitor comparisons, channel analysis, and evidence-based content ideas.
- アプリとCLIで共通の導入手順にまとめ、自然文で分析を始める質問例を追加。 / Unify app and CLI setup instructions and add natural-language research examples.

## 0.1.1 — 2026-10-03

- CodexとClaude Codeの版を揃え、導入・認証・更新の案内を日本語と英語で整備。 / Align client versions and provide Japanese and English installation, authentication, and update guidance.
- 配布物をカタログ・プラグイン定義・利用者向け資料に限定。プラグイン名と接続先は継続。 / Limit the package to catalogs, plugin definitions, and user documentation, preserving the plugin name and endpoint.

## 0.1.0 — 2026-10-03

- Codex・Claude Code向けに、`bazutte`プラグインと`bazutte-plugins`マーケットを追加。 / Add the `bazutte` plugin and `bazutte-plugins` marketplace for Codex and Claude Code.
- 本番エンドポイント`https://bazutte.com/mcp`と、利用者ごとのOAuth認証を設定。 / Configure the production endpoint `https://bazutte.com/mcp` with per-user OAuth authentication.
