---
id: gsi-evacuation-sites-jp
title: gsi-evacuation-sites-jp で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/gsi-evacuation-sites-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット d8ad216、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - mlit-underpass
  - estat-census-mesh-2020
dataset: yuiseki/gsi-evacuation-sites-jp
verified_how: read-data
pattern: questions
finding:
  - 指定緊急避難場所と指定避難所の全国データ(CSV と GeoJSON と GeoParquet)
---

## 要点

- 指定緊急避難場所と指定避難所の全国データ(CSV と GeoJSON と GeoParquet)。毎朝作り直される上書き型で、1回分の取得を置く。
- 分類: 日本の統計・公的GIS。元の情報源: 国土地理院「指定緊急避難場所・指定避難所」。
- 権利: 国土地理院コンテンツ利用規約(PDL1.0、CC BY 4.0 互換)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d8ad216（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 177.4 MB、ファイル 15 本 |
| Parquet | 2 本、合計 9.8 MB、最大 5.7 MB |
| 行数 | 199,263（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/sites.parquet`） | 18（うち文字列 6） |
| 行グループ数（標本の最大） | 2 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `remarks` 97.1% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: sites.parquet、shelters.parquet。他のファイルは未検査） |

## 答えうる問い

- 避難所の密度と人口・浸水域との関係
- 災害種別ごとの避難場所の数

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | CSV の全セル(3,086,388)が Parquet と一致するとカードが検証 | — |
| 幾何 | 点の GeoParquet | — |
| 時点 | — | 上書き型。取得日で件数が変わる。引用には日付を添える |
| 範囲 | — | 自治体が登録し公開に同意したものだけ。全国の全避難所ではない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/gsi-evacuation-sites-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/gsi-evacuation-sites-jp?blobs=true`）と Parquet フッターの取得（2026-10-24）
