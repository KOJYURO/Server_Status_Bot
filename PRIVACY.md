# Privacy Policy / プライバシーポリシー

## EN

### 1. Scope
This policy applies to the 7DTD Server Status Bot distribution and related status updater scripts.

### 2. Data Collected
The bot may process and store the following data:
- Discord guild ID used for server registration
- Server display name
- Telnet connection info: host, port, password
- Runtime status data retrieved from game server commands (for example: day, game time, online count)
- Command execution metadata required for operation logs

### 3. Purpose of Use
Data is used only for:
- Maintaining guild-scoped server registry
- Retrieving game status from telnet
- Building Rich Presence text output
- Basic operation troubleshooting

### 4. Storage
- Persistent registry: `runtime/server_registry.db`
- Runtime status cache: `runtime/status.json`
- Password values are masked in command output, but stored in DB for telnet authentication.

### 5. Sharing
This bot does not intentionally share collected server data with third-party services by default.
If the operator adds external integrations, the operator is responsible for disclosure and consent.

### 6. Retention and Deletion
- A guild registration can be deleted via `/server mode:delete`.
- Operators can remove local files to fully clear stored data.

### 7. Security Notes
- Restrict file access permissions for runtime files.
- Keep host environment secured and patched.
- Use network-level restrictions for telnet when possible.

### 8. Contact
For support, use the project support Discord link documented in README.

---

## JP

### 1. 適用範囲
本ポリシーは 7DTD Server Status Bot と付属の status updater スクリプトに適用されます。

### 2. 取得・保存する情報
本ボットは運用上、次の情報を処理・保存する場合があります。
- サーバー登録に使う Discord guild ID
- サーバー表示名
- Telnet 接続情報（host / port / password）
- ゲームサーバーから取得した実行時ステータス（例: day / game time / online数）
- 動作ログに必要なコマンド実行メタ情報

### 3. 利用目的
情報は次の目的でのみ利用します。
- guild単位サーバー登録の維持
- Telnet からのゲームステータス取得
- Rich Presence 文面の生成
- 基本的な障害調査

### 4. 保存先
- 永続レジストリ: `runtime/server_registry.db`
- 実行時ステータス: `runtime/status.json`
- password はコマンド出力ではマスクされますが、telnet認証のためDBには保存されます。

### 5. 第三者提供
標準構成では、取得したサーバー情報を意図的に第三者サービスへ送信しません。
外部連携を追加した場合は、運用者の責任で告知と同意取得を行ってください。

### 6. 保持期間と削除
- `/server mode:delete` で guild の登録情報を削除できます。
- ローカルファイルを削除することで保存データを完全削除できます。

### 7. セキュリティ注意点
- 実行ファイル・DBの権限を適切に制限してください。
- ホストOSを最新状態に保ってください。
- 可能なら Telnet 接続にネットワーク制限を設けてください。

### 8. 連絡先
サポート窓口は README に記載の Support Discord を参照してください。
