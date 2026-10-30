---
id: fagus-crenata-masting-jp-2026-06
title: fagus-crenata-masting-jp-2026-06 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/fagus-crenata-masting-jp-2026-06 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
  - Hugging Face API と Parquet のフッター（コミット db40a09、2026-10-30）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-30
related:
  - landsat5-fagus-crenata-sites-jp-2026-10
  - agera5-japan-monthly-temperature-1979-2026
  - akita-vegetation-2024
dataset: yuiseki/fagus-crenata-masting-jp-2026-06
verified_how: read-data
pattern: questions
finding:
  - ブナの種子生産の調査データ（東北98地点と北海道渡島半島4地点、1989〜2008年）の凍結コピー
---

## 要点

- ブナの種子生産の調査データ（東北98地点と北海道渡島半島4地点、1989〜2008年）の凍結コピー。4つのCSV（調査地102、種子の豊凶ランクと気象の手がかり102、鹿沼沢の種子トラップ19、モデルの推定値6,747）を、`NA` をnullにした Parquet 4本にした。元の zip も併置。
- 分類: ブナの豊凶。元の情報源: Dryad「Data on seed production from 102 Fagus crenata sites in northern Japan and process model parameters」（Masaki et al.、DOI 10.5061/dryad.7sqv9s54n、版5、2026-06-05）。
- 権利: CC0 1.0（Dryad の記録）。

## 規模と形（2026-10-30 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット db40a09（最終更新 2026-10-28、2026-10-30 に API で確認） |
| Hugging Face のライセンスタグ | cc0-1.0 |
| 全体 | 1.2 MB、ファイル 12 本 |
| Parquet | 4 本、合計 0.4 MB、最大 0.4 MB |
| 行数 | 6,970（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/model_estimates.parquet`） | 10（うち文字列 3） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: model_estimates.parquet。他のファイルは未検査） |

## 答えうる問い

- ブナの豊凶（種子ランク）の年変動と地点間の同調
- 豊凶を予測する過程モデルの推定値の参照

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | CSV を別の方法（DuckDB、全列テキスト）で読み直し、全セルが Parquet と一致（102、102、19、6,747行）とカードが述べる | — |
| 文字 | 調査地名はローマ字と日本語の両方を持つ。元の CSV は BOM つき UTF-8 | — |
| 不明の値 | — | 種子ランクに -1 が61セルある（1999年の54、2004年の7）。元の README はランク0〜3と NA しか定義せず、-1 の意味は不明。ランクとして読まない（カード） |
| 欠測 | — | ランクの列に `NA` が60（1989〜1993年、2004〜2008年）。nullにしてある |
| 尺度 | — | `T.HSM`・`T.LSP` は種子ランク表では標準化（平均0・標準偏差1）だが、鹿沼沢の表では標準化されておらず（T.HSM は 0〜180.7、T.LSP は -95.3〜-0.3）、元の列の説明と食い違う。元のまま |
| 形 | — | `model_estimates` は縦持ちで、地点ごとのパラメータ数が違う（44〜68）。同じ組ではない |
| 範囲 | — | 102地点の気候平均（WorldClim 由来）は別の Zenodo の記録で、含まれない |
| 取得 | — | Dryad は匿名スクリプトを拒むため、zip は手作業でブラウザから取得し、SHA-256 を Dryad の API と照合した |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/fagus-crenata-masting-jp-2026-06 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
- Hugging Face API（`/api/datasets/yuiseki/fagus-crenata-masting-jp-2026-06?blobs=true`）と Parquet フッターの取得（2026-10-30）
