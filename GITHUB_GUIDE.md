# 7DTD Server Status Bot - GitHub Guide (EN)

## Overview

This bot provides rotating Rich Presence text for 7 Days to Die.
Server registration is managed by guild in a SQLite registry, and Presence source guild can be selected by policy.

## Core Commands

- `/help`
- Purpose: Show command descriptions and support links.

- `/presence_now`
- Purpose: Show the currently displayed Rich Presence text.

- `/presence_switch`
- Purpose: Admin command to switch template mode (`list`, `next`, `prev`, `set`).

- `/server`
- Purpose: Admin command to manage telnet config per guild.
- `mode:register` requires `host` and `password`.
- Optional fields: `port` (default: `8081`), `server_name`.
- `mode:show` returns masked password output.
- `mode:delete` removes current guild registration.
- `mode:list` shows summary for registered guilds.
- `mode:list` can be restricted to one development guild by `SERVER_LIST_ALLOWED_GUILD_ID`.

## Data Files

- `runtime/presence_content.json`
- Controls Rich Presence activity type and templates.

- `runtime/server_registry.db`
- Stores guild-scoped server configs and Presence selection state.

- `runtime/status.json`
- Runtime status used to format Rich Presence output.
- Includes `game_datetime` and `horde_countdown_hours` for richer templates.

## Template Placeholders

- `{server}` `{day}` `{game_time}` `{game_datetime}` `{biome}` `{online}` `{horde_eta}` `{horde_countdown_hours}`

## Presence Source Selection

- `PRESENCE_SOURCE_GUILD_MODE=latest_updated|manual|round_robin`
- `PRESENCE_TARGET_GUILD_ID=` (used only in `manual` mode)

Behavior:

- `latest_updated`: picks most recently updated guild config.
- `manual`: uses fixed guild from `PRESENCE_TARGET_GUILD_ID`.
- `round_robin`: cycles across enabled guild configs.

## Support Links

- Mod Support Bot
https://discord.com/oauth2/authorize?client_id=1452050154747203808

- Support Discord
https://discord.gg/FWZHPbFeAg

- Steam Group
https://steamcommunity.com/groups/7DTD_JP

- Privacy Policy
https://github.com/KOJYURO/Server_Status_Bot/blob/main/PRIVACY.md

- Terms of Use
https://github.com/KOJYURO/Server_Status_Bot/blob/main/TERMS.md

## Privacy / Terms Notes

- Local DB stores server connection settings required for status retrieval (host, port, telnet password).
- Password is masked in command output, but stored in DB for telnet login.
- Review and customize policy documents before public distribution.

---

# 7DTD Server Status Bot - GitHubガイド (JP)

## 概要

7 Days to Die の Rich Presence を巡回表示するボットです。
サーバー登録は guild 単位で SQLite に保存し、どの guild 情報を Presence へ出すかをポリシーで選択できます。

## 主要コマンド

- `/help`
- 用途: コマンド説明とサポートリンクを表示します。

- `/presence_now`
- 用途: 現在の Rich Presence 表示文面を確認します。

- `/presence_switch`
- 用途: 管理者向け。テンプレートを切替 (`list`, `next`, `prev`, `set`) します。

- `/server`
- 用途: 管理者向け。guildごとの Telnet 設定を管理します。
- `mode:register` の必須: `host`, `password`。
- 任意項目: `port`（既定 `8081`）, `server_name`。
- `mode:show` は password をマスク表示します。
- `mode:delete` は現在 guild の登録を削除します。
- `mode:list` は登録済み guild の要約を表示します。
- `mode:list` は `SERVER_LIST_ALLOWED_GUILD_ID` で開発 guild 限定にできます。

## データファイル

- `runtime/presence_content.json`
- Rich Presence の activity type とテンプレート文面を管理します。

- `runtime/server_registry.db`
- guild 単位のサーバー設定と Presence 選択状態を保存します。

- `runtime/status.json`
- Rich Presence 文面フォーマットに使う実行時ステータスです。
- `game_datetime` と `horde_countdown_hours` を含めた表示に対応します。

## テンプレートプレースホルダ

- `{server}` `{day}` `{game_time}` `{game_datetime}` `{biome}` `{online}` `{horde_eta}` `{horde_countdown_hours}`

## Presence 出力元の選択

- `PRESENCE_SOURCE_GUILD_MODE=latest_updated|manual|round_robin`
- `PRESENCE_TARGET_GUILD_ID=`（`manual` モード時のみ利用）

動作:

- `latest_updated`: 直近更新 guild を採用
- `manual`: `PRESENCE_TARGET_GUILD_ID` を固定参照
- `round_robin`: 有効 guild を巡回

## サポートリンク

- Mod Support Bot
https://discord.com/oauth2/authorize?client_id=1452050154747203808

- Support Discord
https://discord.gg/FWZHPbFeAg

- Steam Group
https://steamcommunity.com/groups/7DTD_JP

- Privacy Policy
https://github.com/KOJYURO/Server_Status_Bot/blob/main/PRIVACY.md

- Terms of Use
https://github.com/KOJYURO/Server_Status_Bot/blob/main/TERMS.md

## プライバシー / 利用規約メモ

- ステータス取得に必要な接続情報（host / port / telnet password）をローカルDBに保存します。
- コマンド出力では password をマスクしますが、telnet接続のためDBには実値を保存します。
- 公開配布する場合はポリシー文書の内容を運用に合わせて確認・更新してください。
