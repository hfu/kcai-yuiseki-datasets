---
id: microsoft-building-footprints-kanto-2026-08-13
title: microsoft-building-footprints-kanto-2026-08-13 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/microsoft-building-footprints-kanto-2026-08-13 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 6d86dea、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - esa-worldcover-tokyo-2021-100m
  - ghsl-japan-core-2020-30arcsec
dataset: yuiseki/microsoft-building-footprints-kanto-2026-08-13
verified_how: read-data
pattern: questions
finding:
  - 東京・東関東の2つの QuadKey の機械検出の建物の多角形5,781,554件（`height`・`confidence`・`quadkey`）
---

## 要点

- 東京・東関東の2つの QuadKey の機械検出の建物の多角形5,781,554件（`height`・`confidence`・`quadkey`）。QuadKey ごとの GeoParquet と、元の gzip の GeoJSONL を併置。
- 分類: 人口・建物・土地被覆。元の情報源: Microsoft Global ML Building Footprints（2026-08-13のインデックス、QuadKey 133002112・133002113）。
- 権利: Hugging Face のタグは other（CDLA-Permissive-2.0。本文の同梱が必要）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 6d86dea（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 840.2 MB、ファイル 11 本 |
| Parquet | 2 本、合計 390.5 MB、最大 273.2 MB |
| 行数 | 5,781,554（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/buildings-quadkey-133002113.parquet`） | 4（うち文字列 1） |
| 行グループ数（標本の最大） | 392 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: buildings-quadkey-133002113.parquet。他のファイルは未検査） |

## 答えうる問い

- 関東の建物の数・密度・面積の分布（検出ベース）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 件数 | カードの件数5,781,554と一致（実測） | — |
| 分割 | QuadKey ごとの2ファイルで、行グループ392と細かく分かれる | — |
| 意味 | — | 画像由来の予測で、建物台帳ではない。古い画像や欠けた画像があり、見落としと誤検出がありうる。件数を現存する建物の数として扱わない |
| 値 | — | `height` は推定の高さ（m）、`confidence` は検出のスコアで高さの確からしさではない。`-1` は推定なし |
| 識別子 | — | 建物の恒久的な ID が無く、後のリリースと行を結べない |
| 範囲読み(実測) | — | QuadKey 133002112 の渋谷付近（5,657棟）の bbox 読みで 273.2MB／全体273.2MB（全量）、行グループ392でも飛ばせなかった。QuadKey 133002113 は経度139.92〜140.62°・緯度35.46〜36.03° の範囲で、範囲外の窓は0件 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/microsoft-building-footprints-kanto-2026-08-13 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/microsoft-building-footprints-kanto-2026-08-13?blobs=true`）と Parquet フッターの取得（2026-10-26）
