# Local AI Team JP Model Registry

このリポジトリは、アプリ「Local AI Team JP」が参照するモデル一覧を配信します。

- `v1/registry.json`: モデル一覧（schema v1）
- `v1/registry.json.sig`: Ed25519 署名
- `eval/ja_eval_v1.json`: 日本語AIスコアの評価セット（30問・6カテゴリ）
- `eval/core_eval_v1.json`: 基礎能力スコアの評価セット（30問・5カテゴリ、英語中心）
- `eval/results/`: 採点の根拠（各問の回答・ルール採点・判定AIの点数と理由）

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

## スコアについて

2つのスコアは、どちらも実機（Google Pixel 6 / Android 17）で、アプリと同じ実行環境・量子化済みのファイル・temperature 0 で生成した回答を、ルール採点40%＋判定AI60%で採点した値です。

- **日本語AIスコア**（`ja-eval-v1`）: 日本語での使い勝手。会話・敬語・要約・文章作成・日英翻訳・コード。
- **基礎能力スコア**（`core-eval-v1`）: 日本語以外の力。推論・計算・指示の遵守・コード・長文の読み取りを、英語と言語に依存しない問題で測ります。

30問なので、数点の差は誤差とお考えください。

このファイルには、モデル名、配布元の URL、SHA-256、ライセンスの情報だけが含まれます。利用者のデータは含まれません。
