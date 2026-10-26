---
id: ctrees-agb-hokkaido-east-100m
title: ctrees-agb-hokkaido-east-100m で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ctrees-agb-hokkaido-east-100m のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット e0edd7c、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - forty-hokkaido-east-2020
  - gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2
  - gpw-grasslands-hokkaido-east-2018-2020-250m
  - gebco-2026-hokkaido-east-15as
dataset: yuiseki/ctrees-agb-hokkaido-east-100m
verified_how: read-data
pattern: questions
finding:
  - 東部北海道の固定の長方形窓で、CTrees の地上部バイオマス（AGB）と不確かさを、10×10画素のブロックごとに集約した多角形（43,550件）
---

## 要点

- 東部北海道の固定の長方形窓で、CTrees の地上部バイオマス（AGB）と不確かさを、10×10画素のブロックごとに集約した多角形（43,550件）。2010年と2025年の平均・標準偏差・不確かさ・有効画素数を持つ。元の4つの窓の COG も併置。
- 分類: 北海道東部の窓抽出。元の情報源: CTrees 地上部バイオマス（AWS ctrees-agb-100m-global）の2010年・2025年の窓（143〜147°E、42〜46°N）。
- 権利: CC BY 4.0（AWS Open Data Registry の記載）。引用が必要。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット e0edd7c（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 27.9 MB、ファイル 19 本 |
| Parquet | 1 本、合計 2.1 MB、最大 2.1 MB |
| 行数 | 43,550（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/parquet/ctrees_agb_hokkaido_east_2010_2025_1km.parquet`） | 11（うち文字列 0） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 文字の検査 | 文字列の列が無い（検査不要） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: ctrees_agb_hokkaido_east_2010_2025_1km.parquet。他のファイルは未検査） |

## 答えうる問い

- 東部北海道の森林バイオマス量の空間分布
- 2010年と2025年の推定値の比較（変化として読むときの注意あり）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何・座標系 | GeoParquet（`geo` あり、CRS あり）。ブロックの位置は `cell_row`・`cell_col` で元の窓に戻れる | — |
| 再現性 | `scripts/`・`tests/`・`uv.lock`・`source/MANIFEST.json`（SHA-256）を同梱 | — |
| 意味 | — | モデル推定で、現地測定ではない。早い年の推定や参照試料の少ない地域は時間外挿に依存する。2010年と2025年の差を、不確かさを見ずに変化の観測として読まない（カードの注意） |
| 範囲 | — | 島や森林の輪郭ではなく固定の長方形で、海も含む。ブロックは角度格子で、等積ではない（44°Nで約989m×712m） |
| 単位 | — | 不確かさ（`uncertainty_mean`）は画素ごとの標準誤差で、ブロック内の標準偏差（`agb_std`）とは別の量 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- AWS の元データのライセンスの細部（カードの DataCite の記述）は読み切っていない

## 出典

- yuiseki/ctrees-agb-hokkaido-east-100m のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/ctrees-agb-hokkaido-east-100m?blobs=true`）と Parquet フッターの取得（2026-10-26）
