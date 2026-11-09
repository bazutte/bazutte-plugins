# Changelog / 更新履歴

## 0.9.0 — 2026-11-07

- Include an Apache License 2.0 `LICENSE` and add `license` and search `keywords` to both plugin manifests. The license grants no rights to the Bazutte name or logo trademarks, and the Bazutte terms continue to govern use of the service. / Apache License 2.0の`LICENSE`を同梱し、両方のプラグイン定義に`license`と検索用の`keywords`を追加。Bazutteの名前とロゴの商標を使う権利は含まない。サービスの利用には引き続きBazutteの利用規約が適用される。
- Add plugin icons for light and dark themes (`logo.png` and `icon.png` in `plugins/bazutte/assets/`). / プラグインのアイコン（`plugins/bazutte/assets/`のライト用・ダーク用の`logo.png`と`icon.png`）を追加。
- Add a plugin README (`plugins/bazutte/README.md`, describing what the plugin does, what data it sends, and how to get support in English and Japanese) and add directory listing fields (icon and documentation, support, privacy policy, and terms URLs) to the Claude plugin manifest. / プラグインのREADME（`plugins/bazutte/README.md`。できること・送るデータ・連絡先を英語と日本語で説明）を追加し、Claude用のプラグイン定義にディレクトリの掲載項目（アイコン・使い方・お問い合わせ・プライバシーポリシー・利用規約のURL）を追加。
- Make English the default language: `README.md` is now English and the Japanese guide moves to `README.ja.md`. Descriptions in the manifests and this changelog list English first. / 英語を既定の言語に変更。`README.md`を英語にし、日本語の案内は`README.ja.md`へ移した。プラグイン定義の説明とこの更新履歴も英語を先に書く。

## 0.8.6 — 2026-10-31

- When `get_video_ranking` accepts `filters.keywords`, search videos by keyword or genre across titles, tags, and channel names (all words must match, partial and case-insensitive), matching the web page's keyword search; fall back to `filters.title_contains` otherwise. Also add filtering by duration (`min_duration_seconds`, `max_duration_seconds`) and reading `tags`. / 動画ランキング（`get_video_ranking`）が`filters.keywords`を受け付けるサーバーでは、キーワードやジャンルから動画を探すときにタイトルだけでなくタグ・チャンネル名も含めて探す手順に変更。Web画面の「キーワード・ジャンル・タイトル」検索と同じ全語ANDの部分一致で、受け付けないサーバーでは`filters.title_contains`を使う。尺（`min_duration_seconds`・`max_duration_seconds`）での絞り込みと、`tags`の取得も追加。

## 0.8.5 — 2026-10-31

- Read long-running uploads (published more than 30 days ago and still gaining views in the last 7 days, up to 10 per type) from the `long_term_posts` section of `get_channel_detail` when the server returns it. It matches the web page's long-term tab; on servers without it, keep pointing to the web page. / チャンネル詳細（`get_channel_detail`）が`long_term_posts`セクションを返すサーバーでは、公開が30日より前で直近7日間に再生が増えた投稿（長期再生）を種別ごとに最大10本ずつそこから読む手順を追加。Web画面の「長期再生」タブと同じ内容で、返さないサーバーではWeb画面で見られると伝える。

## 0.8.4 — 2026-10-31

- Follow the server's channel-history contract: specify the period with `history.days` only (default and maximum 730), which returns daily rows under 180 days and monthly rows from 180 days. Remove the `granularity` argument. / チャンネル詳細の推移は`history.days`（既定・最大730日）だけで期間を指定し、180日未満は日ごと・180日以上は月ごとで返るサーバーの仕様に合わせた。`granularity`の指定を削除。

## 0.8.3 — 2026-10-31

- Read subscriber, total-view, and upload-count trends from the `history` section of `get_channel_detail` when the server returns it (monthly over the last 730 days by default, daily with `granularity: "daily"` for up to 180 days). On servers without it, keep pointing to the web page. Per-video metric history and descriptions are still not returned. / チャンネル詳細（`get_channel_detail`）が`history`セクションを返すサーバーでは、登録者数・総再生数・投稿数の推移（既定は直近730日の月ごと、`granularity: "daily"`で日ごと・最大180日）をそこから読む手順を追加。返さないサーバーでは従来どおりWeb画面で見られると伝える。動画ごとの指標履歴と説明文は引き続き返さない。

## 0.8.2 — 2026-10-31

- Update call limits to the server's current values (60 per minute per user for every tool), note that `CHANNEL_NOT_FOUND` does not consume the usage quota, and add that daily trends and video descriptions are not returned over MCP, that the AI should not guess tool names for them, and that channel trends are viewable on the web. / 呼び出し回数の上限をサーバーの現在値（どのツールも1ユーザー毎分60回）に直し、`CHANNEL_NOT_FOUND`は利用枠を消費しないことに合わせた。推移や動画の説明文はMCPでは返さず、推移を返すツール名を推測して呼ばないこと、チャンネルの推移はWeb画面で見られることを追加。

## 0.8.1 — 2026-10-31

- Convert date and time arguments such as "2026年7月1日" or "last month" to `YYYY-MM-DD` (Japan time) or `YYYY-MM-DDTHH:MM:SS+09:00` before sending, resolve relative dates from the current time, send both bounds of a period, and retry only once after a rejection. / 日付・日時の引数は、利用者の「2026年7月1日」「先月」などを西暦の`YYYY-MM-DD`（日本時間）か`YYYY-MM-DDTHH:MM:SS+09:00`に直して送る手順を追加。相対表現は現在日時から絶対日付に直し、期間は下限と上限の両方を送り、断られたら1回だけ直す。

## 0.8.0 — 2026-10-17

- Remove steps that relied on video history (`get_video_history`), performance trends (`get_channel_performance_trends`), and channel-detail daily statistics and upload counts (`statistics`), which the server no longer returns. When asked, say they are unavailable and offer what the last-30-day changes and ranking growth can answer. / サーバーが動画の指標履歴（`get_video_history`）、公開後の伸び方の比較（`get_channel_performance_trends`）、チャンネル詳細の日ごとの推移と投稿件数（`statistics`）を返さなくなったため、それらを使う手順を削除。求められたときは取得できないと伝え、直近30日の増分や動画ランキングの増分で答えられる範囲を示す。
- Update upload-list steps: `get_channel_videos` now returns only recently updated uploads (roughly the latest 100 per type) and no longer defaults to the last 30 days. / 投稿一覧（`get_channel_videos`）が直近に更新された投稿（種別ごとにおおむね最新100本）だけを返し、期間を省略しても直近30日に絞らなくなったことに合わせて手順を更新。

## 0.7.0 — 2026-10-17

- Pass `@handle`s and channel URLs directly as `channel_id` (and ranking `channel_ids`) when the server accepts them, skipping the `get_channels` lookup; keep resolving to IDs on servers that accept only `UC…` IDs. / `channel_id`が`@handle`・チャンネルURLを受け付けるサーバーでは、`get_channels`でIDを引かずにそのまま渡す手順に変更。動画ランキングの`channel_ids`も同じ。`UC…`だけを受け付けるサーバーでは従来どおりIDへ解決する。
- Read daily growth from per-snapshot differences when video history returns them, otherwise show cumulative differences with the snapshot interval. / 動画の推移に直前の記録日からの増分が返る場合はその値で日ごとの伸びを読み、返らない場合は記録の間隔を添えて累計の差を示す手順を追加。
- Follow tool descriptions for upload period limits and performance-trend ages and counts, retry period errors with `suggested_request`, and explain `engagement_rate` and `views_per_day`. / 投稿一覧の期間上限、公開後の比較日数・本数をツール説明に従う形にし、期間超過エラーの`suggested_request`で取り直す手順と、`engagement_rate`・`views_per_day`の読み方を追加。

## 0.6.0 — 2026-10-16

- Identify channels by passing `@handle`s, channel URLs, and IDs directly in one request instead of matching by name, and look up video history from a video URL. / `@handle`・チャンネルURL・IDを変換せずにまとめて渡してチャンネルを特定する手順に変更し、名前経由で照合する回り道を削除。動画URLから動画の推移を調べる手順も追加。
- Add steps to find competitors from the top 100 similar channels, compare upload performance by views at 1, 3, 7, and 28 days after publication, and find a channel's outlier uploads by hit score. / 類似チャンネルTop100から競合を探す手順と、公開後1・3・7・28日時点の再生数分布で投稿の伸び方を比べる手順を追加。チャンネル内で普段より伸びた投稿をヒットスコア順で探す手順も追加。
- Cover channel-detail section selection, fetching truncated sections with `next_request`, using `invalid_fields`, `retry_after_seconds`, and `suggested_request` from errors, and restarting pagination after a ranking refresh. / チャンネル詳細のセクション選択と、省略された続きを`next_request`で取得する手順、エラーの`invalid_fields`・`retry_after_seconds`・`suggested_request`の使い方、ランキングのページ送り中に更新された場合の取り直しを追加。
- Explain the subscriber growth-rate denominator and the difference between hit score and the per-age median ratio, and update rate limits to match the current server. / 登録者増加率の分母、ヒットスコアと公開後日数別の中央値比の違いを明記し、呼び出し回数の上限を最新のサーバーに合わせて更新。

## 0.5.0 — 2026-10-15

- Add steps to identify a channel from its URL, ID, or former name and continue to details, uploads, and video metric history, including how to verify a channel known only by its `@handle`. / チャンネルURL・ID・旧チャンネル名からチャンネルを特定し、詳細・投稿一覧・動画の指標履歴へ進む手順を追加。`@handle`しか分からない場合の確かめ方も明記。
- Add steps to pick competitors from the top 100 related channels and compare up to 100 channels at once, and to find channels and videos from keywords. / 関連チャンネルTop100から候補を選び、最大100チャンネルをまとめて比較する手順と、キーワードからチャンネル・動画を探す手順を追加。
- Cover weekly, monthly, and quarterly ban and rename reports and how to read a channel's ban risk. / BAN・改名の週次・月次・四半期レポートと、チャンネル詳細のBANリスクの読み方を追加。
- Use the last 30 days for uploads when no period is given, stating the period instead of waiting for confirmation. / 投稿一覧で期間の指定がなければ確認を待たずに直近30日を使い、採用した期間を示すように変更。
- Clarify that full-field requests split pages while other requests narrow fields after a response-too-large error, and document per-tool rate limits. / 応答が大きすぎる場合は、全項目の依頼なら件数を減らしてページを分け、それ以外は列を絞るように整理。ツールごとの呼び出し回数の上限を追記。
- Expand the research skill description with requests such as channel URLs, name changes, ban risk, keywords, and related channels. / 調査skillの説明に、チャンネルURL・名前変更・BANリスク・キーワード・関連チャンネルなどの依頼例を追加。

## 0.4.2 — 2026-10-13

- Remove research-skill guidance for the connection-check `ping` tool, which the server no longer provides. / サーバー側で廃止した接続確認用の`ping`ツールへの案内を調査skillから削除。

## 0.4.1 — 2026-10-13

- Add guidance to retry once with narrowed keyword rank and related-channel fields instead of repeating the same call after a response-too-large error. / 応答が大きすぎるエラーでは同じ呼び出しを繰り返さず、チャンネル詳細のキーワード順位と関連チャンネルの項目を絞って1回だけ再試行する手順を追加。
- Retrieve full-field pages of 50 or fewer and save reports from the file when the AI client offloads a large result. / 全項目の取得を1ページ50件以下に分け、AIクライアントが大きな結果をファイルへ退避した場合はそのファイルから資料を保存する手順を追加。
- Set the default report location to `bazutte-reports/` in the working directory. / 資料の既定の保存先を作業ディレクトリ直下の`bazutte-reports/`に設定。

## 0.4.0 — 2026-10-05

- Rename the research skill to `bazutte-research`; update invocations using the previous name. / 調査skillを`bazutte-research`へ改名。旧名の呼び出しは新しい名前へ変更してください。
- Clarify Bazutte as the provider, distinguish YouTube-sourced information from custom metrics, and preserve data timestamps. / Bazutteの提供主体、YouTube由来の情報と独自指標の区別、データの時点を明記。
- Add terms and privacy links and explain AI-client data sharing, disconnection, retention, and redistribution. / 利用条件・プライバシーへのリンク、AIクライアントへのデータ共有、接続解除、保存・再配布の説明を追加。

## 0.3.0 — 2026-10-05

- Add report retrieval and saving instructions that preserve every returned field, with a fallback for servers without report support. / 全取得項目を残す資料の取得・保存と、未対応サーバーでの代替手順を追加。
- Explain thumbnails and score metrics, distinguish linked images from embedded files, and verify counts across pages. / サムネイル・拡散率・ヒットスコアの表示、画像の外部参照と埋め込みの区別、ページをまたぐ件数確認を明記。
- Cover keyword rankings, name changes, stored ban and reinstatement history, and capability guidance based on available tools. / キーワード、名称変更、BAN・復旧の履歴の調査と、利用可能なツールに基づく使い方の案内を追加。

## 0.2.0 — 2026-10-04

- Bundle `youtube-research` for video discovery, competitor comparisons, channel analysis, and evidence-based content ideas. / 動画の発見・競合比較・チャンネル分析から企画の根拠まで調べる`youtube-research`を同梱。
- Unify app and CLI setup instructions and add natural-language research examples. / アプリとCLIで共通の導入手順にまとめ、自然文で分析を始める質問例を追加。

## 0.1.1 — 2026-10-03

- Align client versions and provide Japanese and English installation, authentication, and update guidance. / CodexとClaude Codeの版を揃え、導入・認証・更新の案内を日本語と英語で整備。
- Limit the package to catalogs, plugin definitions, and user documentation, preserving the plugin name and endpoint. / 配布物をカタログ・プラグイン定義・利用者向け資料に限定。プラグイン名と接続先は継続。

## 0.1.0 — 2026-10-03

- Add the `bazutte` plugin and `bazutte-plugins` marketplace for Codex and Claude Code. / Codex・Claude Code向けに、`bazutte`プラグインと`bazutte-plugins`マーケットを追加。
- Configure the production endpoint `https://bazutte.com/mcp` with per-user OAuth authentication. / 本番エンドポイント`https://bazutte.com/mcp`と、利用者ごとのOAuth認証を設定。
