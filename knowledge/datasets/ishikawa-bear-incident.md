---
id: ishikawa-bear-incident
title: ishikawa-bear-incident で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ishikawa-bear-incident のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット d2b77a2、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - gifu-bear-sighting
  - kyoto-bear-sighting
dataset: yuiseki/ishikawa-bear-incident
verified_how: read-data
pattern: questions
finding:
  - クマの出没データ3,901件を6表の GeoParquet にしたもの
---

## 要点

- クマの出没データ3,901件を6表の GeoParquet にしたもの。R1〜R6（FY2019〜FY2024）の分析マップは原因別の5ファイル、R7の目撃は暦年2025の1ファイル。
- 分類: クマ出没記録。元の情報源: 石川県「石川県クマ出没データ」（石川県オープンデータカタログ、自然環境課）。
- 権利: CC BY（版は示されない）。このデータセットは CC BY 4.0 として提供。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d2b77a2（最終更新 2026-10-26、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 1.2 MB、ファイル 19 本 |
| Parquet | 6 本、合計 0.3 MB、最大 0.2 MB |
| 行数 | 3,901（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/forest_r1_r6.parquet`） | 18（うち文字列 13） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | parquet/forest_r1_r6.parquet: `remarks` U+FFFD 17・二重エンコード疑い 0（2423行中） |

## 答えうる問い

- 石川県のクマ出没を原因別（森林・河川・誘引物・若い個体・大量出没年）に見る

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | WKT と緯度経度が全3,901行で一致（1e-6）とカードが述べる | — |
| 文字 | BOM つき UTF-8の CSV。日本語が読める | — |
| 重複 | — | R1〜R6の5表は、同じ出没の原因別の抽出で、同じ事象が複数の表に入る（3,798行のうち2,224行が他の表と日付・場所・座標を共有）。表を足して出没件数にしてはいけない |
| キー | — | `id` は年ごとに振り直され、1つの表で最大2行が共有する。表を結ぶ鍵にならない |
| コード | — | 集落コード・500mメッシュコードは、表計算ソフトで指数表記になり、1,130行は3桁しか残らず復元できない（テキストのまま保持） |
| 型 | — | 頭数は `1`、`1頭`、`-`、空のテキスト。日付は形式が混在し、2行は Excel のシリアル値、2行は日付なし |
| 文字(実測) | — | `forest_r1_r6` の `remarks`（2,423行）に U+FFFD が17行。元のデータに由来するかは未確認 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/ishikawa-bear-incident のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/ishikawa-bear-incident?blobs=true`）と Parquet フッターの取得（2026-10-26）
