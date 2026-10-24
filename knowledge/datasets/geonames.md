---
id: geonames
title: geonames で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/geonames のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット f113029、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - wikidata-gazetteer
  - jp-admin-2026-09
  - natural-earth
dataset: yuiseki/geonames
verified_how: read-data
pattern: questions
finding:
  - 1,350万地名・1,900万別名・行政階層・小さな表
---

## 要点

- 1,350万地名・1,900万別名・行政階層・小さな表。日付ごとのスナップショットで、元 zip と型付き Parquet(地名辞書は GeoParquet)。
- 分類: 世界の地理。元の情報源: GeoNames のダンプ(夜ごとの版、20261001 など)。
- 権利: CC BY 4.0(GeoNames の表示)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット f113029（最終更新 2026-10-02、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 1.38 GB、ファイル 24 本 |
| Parquet | 7 本、合計 752.7 MB、最大 177.2 MB |
| 行数 | 33,288,976（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/20261001/geoname/part-01.parquet`） | 20（うち文字列 13） |
| 行グループ数（標本の最大） | 192 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `cc2` 99.9%、`elevation` 97.2%、`admin4_code` 90.4%、`admin3_code` 66.6% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | parquet/20261001/geoname/part-02.parquet: `name` U+FFFD 0・二重エンコード疑い 1（2874228行中） |

## 答えうる問い

- 地名から座標・行政区画を引く
- 別名(多言語)で名寄せする

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | 点の GeoParquet。行グループが192あり範囲読みに向く | — |
| 文字コード | UTF-8、多言語の別名も読める | — |
| コード | — | `admin1_code` は主に FIPS で ISO ではない。日本は 01 愛知〜47 沖縄で、ローマ字順であり JIS 順(北海道が01)ではない |
| 欠け | — | `country_code` が空の行が7,112(海洋・大陸など)。人口最大の行は「地球」「アジア」 |
| 版 | — | 夜ごとの版。名前に日付を含むサブセットで固定される |
| 文字(実測) | — | 検査した1ファイル（2,874,228行）の `name` に二重エンコード疑いが1行 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/geonames のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/geonames?blobs=true`）と Parquet フッターの取得（2026-10-24）
