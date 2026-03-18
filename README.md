# Rich Presence Bot (Minimal)

A minimal rotating Rich Presence bot for 7 Days to Die dedicated servers.
This version uses a DB registry per guild and a selectable source-guild policy for global Presence output.

## 1. Features

- Rotating Rich Presence (Game DateTime / Biome / Online / Horde Countdown Hours)
- Rich Presence content managed by JSON: `runtime/presence_content.json`
- Guild-scoped server registry managed by SQLite DB: `runtime/server_registry.db`
- `/help` command with command guide and support links
- `/server` command for guild-scoped telnet registration (register/delete/show/list)
- Source-guild selection logic for global Presence output

## 2. Setup

```bash
cd "/root/Release/Rich Presence Bot"
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

Set `DISCORD_BOT_TOKEN` in `.env`.

Edit:
- `runtime/presence_content.json` for display templates
- `.env` for DB path, source selection mode, and list visibility guild

Available placeholders:
- `{server}` `{day}` `{game_time}` `{game_datetime}` `{biome}` `{online}` `{horde_eta}` `{horde_countdown_hours}`

## 3. Start

```bash
cd "/root/Release/Rich Presence Bot"
source .venv/bin/activate
python3 bot.py
```

## 4. Auto-update status.json from 7DTD Telnet

Updater reads telnet targets from DB per selected guild and writes `status.json`.

One-shot (connection test):

```bash
cd "/root/Release/Rich Presence Bot"
source .venv/bin/activate
python3 scripts/update_status_from_7dtd_telnet.py --once
```

Continuous loop:

```bash
cd "/root/Release/Rich Presence Bot"
source .venv/bin/activate
python3 scripts/update_status_from_7dtd_telnet.py
```

## 5. Source-Guild Selection Logic

Environment variables:

- `PRESENCE_SOURCE_GUILD_MODE=latest_updated|manual|round_robin`
- `PRESENCE_TARGET_GUILD_ID=` (used only when `manual`)

Modes:

- `latest_updated`
- Picks the most recently updated guild config (priority-aware)

- `manual`
- Uses the fixed guild ID from `PRESENCE_TARGET_GUILD_ID`

- `round_robin`
- Cycles across enabled guild configs in DB

## 6. Commands

### 6.1 Admin commands

- `/help` — command guide + support links
- `/presence_now` — show current Presence text
- `/presence_switch mode:list|next|prev|set` — manual template control
- `/server mode:register host:... password:... [port] [server_name]` — register/update current guild config
- `/server mode:show` — show current guild config (password masked)
- `/server mode:delete` — delete current guild config
- `/server mode:list` — show registered guild configs summary

### 6.2 Notes

- `/server register` requires `host` and `password`
- `port` defaults to `8081`
- Registry is DB-based; no restart needed after register/delete
- `/server mode:list` can be restricted to one dev guild via `SERVER_LIST_ALLOWED_GUILD_ID`
- Presence is still one global bot status (Discord limitation)

### 6.3 Support links

- Mod Support Bot: https://discord.com/oauth2/authorize?client_id=1452050154747203808
- Support Discord: https://discord.gg/FWZHPbFeAg
- Steam Group: https://steamcommunity.com/groups/7DTD_JP
- Privacy Policy: [PRIVACY.md](PRIVACY.md)
- Terms of Use: [TERMS.md](TERMS.md)

### 6.4 Privacy and Terms

- This bot stores guild-scoped server config in local DB (`runtime/server_registry.db`).
- Stored fields include host, port, and telnet password required for status retrieval.
- `/server mode:show` masks password output, but DB stores password as-is for connection use.
- See policy docs: [PRIVACY.md](PRIVACY.md), [TERMS.md](TERMS.md)

## 7. systemd

### 7.1 Install

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_install.sh
```

Install and start immediately:

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_install.sh --now
```

### 7.2 Check status

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_status.sh
```

### 7.3 Restart

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_restart.sh
```

---

# Rich Presence Bot (Minimal) - 日本語

7 Days to Die 向けの最小構成 Rich Presence ボットです。
この版では guild_id 単位でDB管理し、どのguildの情報をPresenceへ出すかを選択ロジックで制御します。

## 1. 主な機能

- Rich Presence を巡回表示（Game日時 / Biome / Online / ホード残り時間）
- 表示テンプレートを JSON 管理: `runtime/presence_content.json`
- guild単位サーバー登録を SQLite 管理: `runtime/server_registry.db`
- `/help` でコマンド説明とサポートリンク表示
- `/server` で guildごとのTelnet登録を管理（register/delete/show/list）
- Presence出力元guildを選ぶロジックを実装

## 2. セットアップ

```bash
cd "/root/Release/Rich Presence Bot"
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

`.env` の `DISCORD_BOT_TOKEN` を設定してください。

編集ポイント:
- 表示テンプレート: `runtime/presence_content.json`
- DBパス・出力元選択・list公開範囲: `.env`

利用可能プレースホルダ:
- `{server}` `{day}` `{game_time}` `{game_datetime}` `{biome}` `{online}` `{horde_eta}` `{horde_countdown_hours}`

## 3. 起動

```bash
cd "/root/Release/Rich Presence Bot"
source .venv/bin/activate
python3 bot.py
```

## 4. status.json 自動更新（7DTD Telnet）

Updater は選択されたguildのDB登録情報を使ってTelnet接続し、`status.json` を更新します。

疎通確認（1回実行）:

```bash
cd "/root/Release/Rich Presence Bot"
source .venv/bin/activate
python3 scripts/update_status_from_7dtd_telnet.py --once
```

連続実行:

```bash
cd "/root/Release/Rich Presence Bot"
source .venv/bin/activate
python3 scripts/update_status_from_7dtd_telnet.py
```

## 5. 出力元guildの選択ロジック

環境変数:

- `PRESENCE_SOURCE_GUILD_MODE=latest_updated|manual|round_robin`
- `PRESENCE_TARGET_GUILD_ID=`（`manual` のときのみ利用）

モード:

- `latest_updated`
- 直近更新guildを優先（priority考慮）

- `manual`
- `PRESENCE_TARGET_GUILD_ID` の guild を固定参照

- `round_robin`
- DB内の有効guildを巡回参照

## 6. コマンド

### 6.1 管理者コマンド

- `/help` - コマンド説明とサポートリンク
- `/presence_now` - 現在のPresence文面を表示
- `/presence_switch mode:list|next|prev|set` - テンプレート手動切替
- `/server mode:register host:... password:... [port] [server_name]` - 現在guildの設定を登録/更新
- `/server mode:show` - 現在guildの登録を表示（passwordはマスク）
- `/server mode:delete` - 現在guildの登録を削除
- `/server mode:list` - 登録guildの一覧要約を表示

### 6.2 補足

- `/server register` の必須は `host` と `password`
- `port` 未指定時は `8081`
- 登録情報はDB管理なので register/delete 後の再起動は不要
- `/server mode:list` は `SERVER_LIST_ALLOWED_GUILD_ID` で開発ギルド限定にできます
- Discord仕様上、Presence表示はBot単位で1つのみです

### 6.3 サポートリンク

- Mod Support Bot: https://discord.com/oauth2/authorize?client_id=1452050154747203808
- Support Discord: https://discord.gg/FWZHPbFeAg
- Steam Group: https://steamcommunity.com/groups/7DTD_JP
- Privacy Policy: [PRIVACY.md](PRIVACY.md)
- Terms of Use: [TERMS.md](TERMS.md)

### 6.4 プライバシーと利用規約

- 本ボットは guild 単位のサーバー設定をローカルDB（`runtime/server_registry.db`）に保存します。
- ステータス取得に必要な host / port / telnet password を保持します。
- `/server mode:show` では password をマスク表示しますが、接続用途のためDB上は実値を保持します。
- 詳細は [PRIVACY.md](PRIVACY.md), [TERMS.md](TERMS.md) を参照してください。

## 7. systemd

### 7.1 インストール

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_install.sh
```

起動まで一気に行う場合:

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_install.sh --now
```

### 7.2 状態確認

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_status.sh
```

### 7.3 再起動

```bash
cd "/root/Release/Rich Presence Bot"
sudo ./scripts/systemd_restart.sh
```
