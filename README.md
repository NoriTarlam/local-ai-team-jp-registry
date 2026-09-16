# Local AI Team JP Model Registry

このリポジトリは、アプリ「Local AI Team JP」が参照するモデル一覧を配信します。

- `v1/registry.json`: モデル一覧（schema v1）
- `v1/registry.json.sig`: Ed25519 署名

アプリは、組み込まれた公開鍵で署名を検証できた一覧だけを使います。一覧の `revision` は、更新のたびに必ず上げてください。アプリは、手元にあるものより古い revision を受け付けません。

## 更新手順

アプリのリポジトリで、次の順に実行します。

1. モデル一覧を検証してから、署名します。

   ```bash
   dart run tool/registry_sign.dart sign <path>/v1/registry.json secrets/registry-2026.key
   ```

2. 署名を確認します。

   ```bash
   dart run tool/registry_sign.dart verify <path>/v1/registry.json zCItqunbTO8o5XrR5gN4EKP504iRBoySlk0trHPKVpk=
   ```

3. `v1/registry.json` と `v1/registry.json.sig` の2つをコミットし、push します。

秘密鍵はこのリポジトリに入れないでください。

このファイルには、モデル名、配布元の URL、SHA-256、ライセンスの情報だけが含まれます。利用者のデータは含まれません。
