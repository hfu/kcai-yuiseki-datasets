---
id: agera5-japan-monthly-water-1979-2026
title: agera5-japan-monthly-water-1979-2026 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/agera5-japan-monthly-water-1979-2026 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
  - Hugging Face API と Parquet のフッター（コミット b3d1a83、2026-10-30）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-30
related:
  - agera5-japan-monthly-temperature-1979-2026
  - fagus-crenata-masting-jp-2026-06
dataset: yuiseki/agera5-japan-monthly-water-1979-2026
verified_how: read-data
pattern: questions
finding:
  - 日本周辺の窓の0.1°格子の月別降水量（`precip_mm`）と基準蒸発散量（`et0_mm`、いずれも月合計mm）を、セルの中心点の GeoParquet（47,507,200行、571か月、年ごと48ファイル）にしたもの
---

## 要点

- 日本周辺の窓の0.1°格子の月別降水量（`precip_mm`）と基準蒸発散量（`et0_mm`、いずれも月合計mm）を、セルの中心点の GeoParquet（47,507,200行、571か月、年ごと48ファイル）にしたもの。気温版と同じ格子・窓・列で、`month`・`source_grid_row`・`source_grid_col` で結べる。
- 分類: 気候。元の情報源: Copernicus C3S AgERA5 v2.0 の月降水量（precipitation flux）とFAOの基準蒸発散量（FAO-56 Penman-Monteith、AgERA5由来）。FAO GIS カタログの COG 経由、122〜154°E、20〜46°N。
- 権利: CC BY-SA 4.0（FAO のカタログの表示）。気温版（agera5-japan-monthly-temperature-1979-2026）は CC BY 4.0。

## 規模と形（2026-10-30 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット b3d1a83（最終更新 2026-10-28、2026-10-30 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-sa-4.0 |
| 全体 | 71.9 MB、ファイル 56 本 |
| Parquet | 48 本、合計 71.1 MB、最大 1.5 MB |
| 行数 | 47,507,200（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/year=2017/part-0.parquet`） | 7（うち文字列 0） |
| 行グループ数（標本の最大） | 12 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `et0_mm` 79.0%、`precip_mm` 79.0% |
| 文字の検査 | 文字列の列が無い（検査不要） |

## 答えうる問い

- 日本周辺の月降水量・蒸発散量の長期傾向（1979〜2026年7月）
- 気温版と結んだ水収支（降水−蒸発散）の指標

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 分割 | 年ごとのファイル（`year=YYYY`）で必要な年だけ取れる | — |
| 結合 | 気温版と格子・列が同じで、3列で結べる | — |
| ライセンス | — | CC BY-SA 4.0。気温版（CC BY 4.0）と違い、継承（share-alike）が派生物に及ぶ。結んだ表を再配布するときは条件の確認が要る |
| null | — | 値が入るのは9,993,071で、37,514,129はnull（元の格子は陸のみ。両列で同じセル） |
| 意味 | — | `et0_mm` は AgERA5 から FAO が導いた量で、観測ではない |
| 範囲 | — | 2026年は1〜7月のみ。矩形の窓で、日本の行政境界ではない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/agera5-japan-monthly-water-1979-2026 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
- Hugging Face API（`/api/datasets/yuiseki/agera5-japan-monthly-water-1979-2026?blobs=true`）と Parquet フッターの取得（2026-10-30）
