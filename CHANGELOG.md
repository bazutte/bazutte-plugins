# 更新履歴 / Changelog

## 0.7.0 — 2026-10-17

- `channel_id`が`@handle`・チャンネルURLを受け付けるサーバーでは、`get_channels`でIDを引かずにそのまま渡す手順に変更。動画ランキングの`channel_ids`も同じ。`UC…`だけを受け付けるサーバーでは従来どおりIDへ解決する。 / Pass `@handle`s and channel URLs directly as `channel_id` (and ranking `channel_ids`) when the server accepts them, skipping the `get_channels` lookup; keep resolving to IDs on servers that accept only `UC…` IDs.
- 動画の推移に直前の記録日からの増分が返る場合はその値で日ごとの伸びを読み、返らない場合は記録の間隔を添えて累計の差を示す手順を追加。 / Read daily growth from per-snapshot differences when video history returns them, otherwise show cumulative differences with the snapshot interval.
- 投稿一覧の期間上限、公開後の比較日数・本数をツール説明に従う形にし、期間超過エラーの`suggested_request`で取り直す手順と、`engagement_rate`・`views_per_day`の読み方を追加。 / Follow tool descriptions for upload period limits and performance-trend ages and counts, retry period errors with `suggested_request`, and explain `engagement_rate` and `views_per_day`.

## 0.6.0 — 2026-10-16

- `@handle`・チャンネルURL・IDを変換せずにまとめて渡してチャンネルを特定する手順に変更し、名前経由で照合する回り道を削除。動画URLから動画の推移を調べる手順も追加。 / Identify channels by passing `@handle`s, channel URLs, and IDs directly in one request instead of matching by name, and look up video history from a video URL.
- 類似チャンネルTop100から競合を探す手順と、公開後1・3・7・28日時点の再生数分布で投稿の伸び方を比べる手順を追加。チャンネル内で普段より伸びた投稿をヒットスコア順で探す手順も追加。 / Add steps to find competitors from the top 100 similar channels, compare upload performance by views at 1, 3, 7, and 28 days after publication, and find a channel's outlier uploads by hit score.
- チャンネル詳細のセクション選択と、省略された続きを`next_request`で取得する手順、エラーの`invalid_fields`・`retry_after_seconds`・`suggested_request`の使い方、ランキングのページ送り中に更新された場合の取り直しを追加。 / Cover channel-detail section selection, fetching truncated sections with `next_request`, using `invalid_fields`, `retry_after_seconds`, and `suggested_request` from errors, and restarting pagination after a ranking refresh.
- 登録者増加率の分母、ヒットスコアと公開後日数別の中央値比の違いを明記し、呼び出し回数の上限を最新のサーバーに合わせて更新。 / Explain the subscriber growth-rate denominator and the difference between hit score and the per-age median ratio, and update rate limits to match the current server.

## 0.5.0 — 2026-10-15

- チャンネルURL・ID・旧チャンネル名からチャンネルを特定し、詳細・投稿一覧・動画の指標履歴へ進む手順を追加。`@handle`しか分からない場合の確かめ方も明記。 / Add steps to identify a channel from its URL, ID, or former name and continue to details, uploads, and video metric history, including how to verify a channel known only by its `@handle`.
- 関連チャンネルTop100から候補を選び、最大100チャンネルをまとめて比較する手順と、キーワードからチャンネル・動画を探す手順を追加。 / Add steps to pick competitors from the top 100 related channels and compare up to 100 channels at once, and to find channels and videos from keywords.
- BAN・改名の週次・月次・四半期レポートと、チャンネル詳細のBANリスクの読み方を追加。 / Cover weekly, monthly, and quarterly ban and rename reports and how to read a channel's ban risk.
- 投稿一覧で期間の指定がなければ確認を待たずに直近30日を使い、採用した期間を示すように変更。 / Use the last 30 days for uploads when no period is given, stating the period instead of waiting for confirmation.
- 応答が大きすぎる場合は、全項目の依頼なら件数を減らしてページを分け、それ以外は列を絞るように整理。ツールごとの呼び出し回数の上限を追記。 / Clarify that full-field requests split pages while other requests narrow fields after a response-too-large error, and document per-tool rate limits.
- 調査skillの説明に、チャンネルURL・名前変更・BANリスク・キーワード・関連チャンネルなどの依頼例を追加。 / Expand the research skill description with requests such as channel URLs, name changes, ban risk, keywords, and related channels.

## 0.4.2 — 2026-10-13

- サーバー側で廃止した接続確認用の`ping`ツールへの案内を調査skillから削除。 / Remove research-skill guidance for the connection-check `ping` tool, which the server no longer provides.

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
