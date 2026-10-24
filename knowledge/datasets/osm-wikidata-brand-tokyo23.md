---
id: osm-wikidata-brand-tokyo23
title: osm-wikidata-brand-tokyo23 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/osm-wikidata-brand-tokyo23 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 83e3033、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-wikidata-brand-jp
  - osm-tokyo23-src-2026-08
dataset: yuiseki/osm-wikidata-brand-tokyo23
verified_how: read-data
pattern: questions
finding:
  - 23区の店舗チェーン892ブランド・25,407地物の、OSM 表記と Wikidata 名の対照
---

## 要点

- 23区の店舗チェーン892ブランド・25,407地物の、OSM 表記と Wikidata 名の対照。第2版(第1版は PostGIS 経由で name・brand が列に昇格していた)。
- 分類: OSM とその派生。元の情報源: OSM の brand:wikidata と Wikidata の名前の対照(全国)。
- 権利: ODbL と Wikidata(CC0)の併用。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 83e3033（最終更新 2026-09-17、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 0.6 MB、ファイル 5 本 |
| Parquet | 1 本、合計 0.6 MB、最大 0.6 MB |
| 行数 | 892（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/train-00000-of-00001.parquet`） | 9（うち文字列 8） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: train-00000-of-00001.parquet。他のファイルは未検査） |

## 答えうる問い

- ブランド名の表記ゆれの調査
- OSM のタグ付けの誤りの発見

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 規模 | Parquet 1本(2.2MB) | — |
| 欠陥に見えて欠陥でないもの | — | 店舗の駐車場や駐輪場に `brand:wikidata` が付いて、別の名前に見えることがある。1つのチェーンに Wikidata 項目が2つあるときは両方を残す |
| 件数 | — | 東京23区版の件数とは別物(7-ELEVEN は全国9,698、23区1,512) |
| 欠け | — | 12ブランドは Wikidata ダンプに項目が無い(`found: false`) |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/osm-wikidata-brand-tokyo23 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/osm-wikidata-brand-tokyo23?blobs=true`）と Parquet フッターの取得（2026-10-24）
