---
id: agera5-japan-monthly-temperature-1979-2026
title: agera5-japan-monthly-temperature-1979-2026 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/agera5-japan-monthly-temperature-1979-2026 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 348e459、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - koppen-geiger-east-asia-1991-2020
  - jma-rain-tokyo
dataset: yuiseki/agera5-japan-monthly-temperature-1979-2026
verified_how: read-data
pattern: questions
finding:
  - 日本周辺の窓（長方形、海を含む）の0.1°格子の月別気温を、セルの中心点の GeoParquet（47,507,200行、571か月、年ごと48ファイル）にしたもの
---

## 要点

- 日本周辺の窓（長方形、海を含む）の0.1°格子の月別気温を、セルの中心点の GeoParquet（47,507,200行、571か月、年ごと48ファイル）にしたもの。最高・最低気温はケルビン。
- 分類: 気候。元の情報源: Copernicus C3S AgERA5 v2.0 の月平均最高・最低気温（FAO GIS カタログの COG 経由）、122〜154°E、20〜46°N。
- 権利: CC BY 4.0（C3S）。出典の表示が必要。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 348e459（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 84.6 MB、ファイル 56 本 |
| Parquet | 48 本、合計 83.8 MB、最大 1.8 MB |
| 行数 | 47,507,200（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/year=1980/part-0.parquet`） | 7（うち文字列 0） |
| 行グループ数（標本の最大） | 12 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `tmin_mean_k` 79.0%、`tmax_mean_k` 79.0% |
| 文字の検査 | 文字列の列が無い（検査不要） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: part-0.parquet。他のファイルは未検査） |

## 答えうる問い

- 日本周辺の月平均気温の長期トレンド（1979〜2026年7月）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 分割 | 年ごとのファイル（`year=YYYY`）で、必要な年だけ取れる。行グループ12 | — |
| 幾何 | 点（WKB）、GeoParquet 1.1.0、CRS あり | — |
| null | — | 気温の有効値は9,993,071で、37,514,129はnull（海など NoData のセルを格子の位置のまま保持） |
| 形 | — | セルの中心点で多角形ではない。矩形の窓で、日本の行政境界ではない |
| 単位 | — | ケルビン（`tmax_mean_k`、`tmin_mean_k`）。摂氏への換算は利用側 |
| 範囲 | — | 2026年は1〜7月のみ |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/agera5-japan-monthly-temperature-1979-2026 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/agera5-japan-monthly-temperature-1979-2026?blobs=true`）と Parquet フッターの取得（2026-10-26）
