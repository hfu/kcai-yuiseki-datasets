---
id: geo-triples-jp-gov
title: geo-triples-jp-gov で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/geo-triples-jp-gov のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット df079b5、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - jp-admin-2026-09
  - geo-triples-japan
  - geo-triples-tokyo23
dataset: yuiseki/geo-triples-jp-gov
verified_how: read-data
pattern: questions
finding:
  - 行政区画ポリゴン同士の空間関係(GeoSPARQL の Simple Features 8述語、DE-9IM、RCC8)を1行1三つ組にした表と、文にした表、評価問題
---

## 要点

- 行政区画ポリゴン同士の空間関係(GeoSPARQL の Simple Features 8述語、DE-9IM、RCC8)を1行1三つ組にした表と、文にした表、評価問題。triples 162,810行、cpt 165,670行、probe 1,807行。
- 分類: 日本の統計・公的GIS。元の情報源: jp-admin-2026-09(コミット c86cbe9)の47都道府県と1,909市区町村。
- 権利: CC BY 4.0(share-alike なし)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット df079b5（最終更新 2026-09-26、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 2.3 MB、ファイル 9 本 |
| Parquet | 3 本、合計 2.3 MB、最大 1.5 MB |
| 行数 | 330,287（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/cpt.parquet`） | 15（うち文字列 14） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 市区町村の隣接・包含を表で引く
- 言語モデルの事前学習・評価用に地理の事実を文にする

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 件数 | 実測でカードの3表の行数(162,810/165,670/1,807)と一致 | — |
| キー | IDは `abr-muni-011002` の形で、後ろの6桁が lg_code。幾何の列は無い | — |
| 入力の限定 | — | 入力は jp-admin の1,918から形の無い9件を除いた1,909件。2024年新設の浜松市の3区などは含まれない |
| 向き | — | sfTouches は向きつきの行で、無向の辺にするには半分にする(10,152→5,076) |
| 証明の有無 | — | certified が135,658、uncertified が27,152 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/geo-triples-jp-gov のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/geo-triples-jp-gov?blobs=true`）と Parquet フッターの取得（2026-10-24）
