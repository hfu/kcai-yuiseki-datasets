---
id: ksj-p11-bus-stop-greater-tokyo
title: ksj-p11-bus-stop-greater-tokyo で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ksj-p11-bus-stop-greater-tokyo のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 3ec7ac8、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - ksj-p11-bus-stop-jp
  - ksj-n07-bus-route-greater-tokyo
dataset: yuiseki/ksj-p11-bus-stop-greater-tokyo
verified_how: read-data
pattern: questions
finding:
  - 埼玉・千葉・東京・神奈川のバス停44,101件
---

## 要点

- 埼玉・千葉・東京・神奈川のバス停44,101件。ksj-p11-bus-stop-jp の部分集合。
- 分類: 日本の統計・公的GIS。元の情報源: 国土交通省 国土数値情報 P11 バス停留所(2022年版 第3.0版)。
- 権利: 国土数値情報の利用規約(CC BY 4.0 互換)。2010年版は非商用で含まれない。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 3ec7ac8（最終更新 2026-10-22、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 9.4 MB、ファイル 15 本 |
| Parquet | 5 本、合計 2.5 MB、最大 1.3 MB |
| 行数 | 88,202（全 Parquet のフッターの合計。全国1本と県別の本が同じ地物を二重に持つため、実際の件数はその約半分の 44,101。カードの件数と一致） |
| 列数（代表ファイル `parquet/bus_stop.parquet`） | 9（うち文字列 7） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: bus_stop.parquet、11.parquet。他のファイルは未検査） |

## 答えうる問い

- バス停の密度を県・市区町村ごとに比べる
- 停車系統の数(n_routes)で拠点性を測る

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | 点の GeoParquet。元データと一致するとカードが検証 | — |
| 文字コード | 波ダッシュは GeoJSON 側の表記(U+301C)に揃えてあり、cp932 の dbf を直接読んだときの U+FF5E とは違う | — |
| 範囲 | — | 2022年8月ごろ。デマンドバス・高速バスは無い。`note` が付く348停留所は元で説明が無い |
| 系統名 | — | 系統名は事業者が付けた文字列で、同じ系統が停留所ごとに違う書き方になりうる。停留所を順序のある路線にはつなげない |
| 上下線 | — | 同一事業者・同名・同道路の停留所は元で統合され、道路の両側は多くが1点 |
| 精度 | — | 位置は目視確認の精度 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 重複12件(名称・事業者・座標が同じ)は残されている

## 出典

- yuiseki/ksj-p11-bus-stop-greater-tokyo のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ksj-p11-bus-stop-greater-tokyo?blobs=true`）と Parquet フッターの取得（2026-10-24）
