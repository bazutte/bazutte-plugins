# Changelog

## 0.9.2 — 2026-11-10

- Write the plugin README in English only and link to the Japanese guide.

## 0.9.1 — 2026-11-10

- Rewrite the plugin description and README around what you can ask, and link the homepage and documentation to the English pages.

## 0.9.0 — 2026-11-07

- Include an Apache License 2.0 `LICENSE` and add `license` and search `keywords` to both plugin manifests.
- Add plugin icons for light and dark themes.
- Add a plugin README and directory listing fields (icon, documentation, support, privacy policy, and terms URLs) to the Claude plugin manifest.
- Make English the default: `README.md` is English and the Japanese guide is `README.ja.md`.

## 0.8.6 — 2026-10-31

- Search videos by keyword or genre across titles, tags, and channel names, and filter by duration, when the server supports it.

## 0.8.5 — 2026-10-31

- Read long-running uploads (published over 30 days ago and still gaining views) from channel details when the server returns them.

## 0.8.4 — 2026-10-31

- Follow the server's channel-history contract, which takes only `history.days`.

## 0.8.3 — 2026-10-31

- Read subscriber, total-view, and upload-count trends from channel details when the server returns them.

## 0.8.2 — 2026-10-31

- Update call limits to the server's current values (60 per minute for every tool).

## 0.8.1 — 2026-10-31

- Convert dates such as "last month" to absolute dates in Japan time before sending them.

## 0.8.0 — 2026-10-17

- Remove steps that relied on video history, performance trends, and daily channel statistics, which the server no longer returns.
- Reflect that the upload list now returns only recent uploads (roughly the latest 100 per type).

## 0.7.0 — 2026-10-17

- Pass `@handle`s and channel URLs directly when the server accepts them, without looking up IDs first.
- Add steps for daily video growth, retrying period errors, and reading engagement rate and views per day.

## 0.6.0 — 2026-10-16

- Identify channels from `@handle`s, URLs, and IDs in one request, and look up video history from a video URL.
- Add steps to find competitors from similar channels, compare upload performance after publication, and find a channel's outlier uploads.
- Fetch truncated channel-detail sections and use the fixes suggested in error responses.

## 0.5.0 — 2026-10-15

- Go from a channel URL, ID, or former name to its details, uploads, and video history.
- Compare up to 100 channels at once and find channels and videos from keywords.
- Add ban and rename reports and channel ban risk.
- Use the last 30 days for uploads when no period is given.

## 0.4.2 — 2026-10-13

- Remove guidance for the `ping` tool, which the server no longer provides.

## 0.4.1 — 2026-10-13

- Retry once with fewer fields after a response-too-large error.
- Save full-field reports in pages of 50 or fewer, by default under `bazutte-reports/`.

## 0.4.0 — 2026-10-05

- Rename the research skill to `bazutte-research`; update invocations that use the old name.
- Clarify the provider, data sources, custom metrics, terms, and data sharing with AI clients.

## 0.3.0 — 2026-10-05

- Save reports that keep every returned field, with thumbnails, spreading rate, and hit score.
- Cover keyword rankings, name changes, and ban and reinstatement history.

## 0.2.0 — 2026-10-04

- Bundle the research skill for video discovery, competitor comparisons, and channel analysis.
- Unify app and CLI setup instructions and add example questions.

## 0.1.1 — 2026-10-03

- Align client versions and add installation, authentication, and update guides.

## 0.1.0 — 2026-10-03

- Add the `bazutte` plugin and `bazutte-plugins` marketplace for Codex and Claude Code, connecting to `https://bazutte.com/mcp` with per-user OAuth.
