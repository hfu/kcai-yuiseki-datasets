---
id: geo-triples-japan
title: geo-triples-japan で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/geo-triples-japan のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット bb99ceb、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - geo-triples-tokyo23
  - geo-triples-jp-gov
  - osm-japan-src-2026-08
dataset: yuiseki/geo-triples-japan
verified_how: read-data
pattern: questions
finding:
  - OSM の日本の行政区画とPOIの空間関係の三つ組(triples 3,286,232行)、文(cpt 4,678,910行)、評価問題(probe 68,025行)
---

## 要点

- OSM の日本の行政区画とPOIの空間関係の三つ組(triples 3,286,232行)、文(cpt 4,678,910行)、評価問題(probe 68,025行)。
- 分類: OSM とその派生。元の情報源: osm-japan-src-2026-08(OSM planet 2026-08-31)の国・47都道府県・1,740市区町村・80,748POI。
- 権利: ODbL-1.0。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット bb99ceb（最終更新 2026-09-26、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 86.2 MB、ファイル 9 本 |
| Parquet | 3 本、合計 86.2 MB、最大 62.5 MB |
| 行数 | 8,033,167（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/cpt.parquet`） | 14（うち文字列 13） |
| 行グループ数（標本の最大） | 5 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: cpt.parquet、probe.parquet。他のファイルは未検査） |

## 答えうる問い

- POI が属する市区町村を答える言語モデルの学習・評価
- 観測された関係と合成された関係の区別

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 件数 | 本文の triples 3,286,232 行は、実測(3,286,232)と一致 | — |
| カードの冒頭 | — | 冒頭の段落の件数(510,616・483,922・8,890)は geo-triples-tokyo23 の数字で、このデータセットの実測(3,286,232・4,678,910・68,025)と合わない。本文の表の数字を使う |
| 継承 | — | ODbL の share-alike が派生物に及ぶ(jp-gov と違う点) |
| 合成行 | — | triples の約半分(1,642,824行)は RCC8 の合成表から導いた行で、観測でない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/geo-triples-japan のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/geo-triples-japan?blobs=true`）と Parquet フッターの取得（2026-10-24）
