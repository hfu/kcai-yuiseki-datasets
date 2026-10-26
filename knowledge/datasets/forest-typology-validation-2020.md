---
id: forest-typology-validation-2020
title: forest-typology-validation-2020 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/forest-typology-validation-2020 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット b4cf5ce、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - forty-hokkaido-east-2020
dataset: yuiseki/forest-typology-validation-2020
verified_how: read-data
pattern: questions
finding:
  - ForTy 森林タイプ図の検証用の世界の標本9,100地点を点にした GeoParquet
---

## 要点

- ForTy 森林タイプ図の検証用の世界の標本9,100地点を点にした GeoParquet。全地点（9,100）と、合意で解決した地点（8,190）の2ファイル。元の CSV も併置。
- 分類: 北海道東部の窓抽出。元の情報源: Global Validation of Forest Types (GVFT) 2020 v0.6（Figshare+）。
- 権利: CC BY 4.0。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット b4cf5ce（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 1.6 MB、ファイル 9 本 |
| Parquet | 2 本、合計 0.7 MB、最大 0.3 MB |
| 行数 | 17,290（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/all-sites.parquet`） | 16（うち文字列 0） |
| 行グループ数（標本の最大） | 5 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 文字の検査 | 文字列の列が無い（検査不要） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: all-sites.parquet。他のファイルは未検査） |

## 答えうる問い

- 森林タイプ図の精度評価に使う世界の標本地点
- 層（strata）ごとの標本の偏り

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| キー・分布 | `sampleid` は一意。`strata` は1〜7が1,300件ずつの均衡 | — |
| 幾何 | 点の GeoParquet。`geo` メタデータに CRS は無い（カードは EPSG:4326 の点と述べる）。`lon`・`lat` も保持 | — |
| 北海道東部との関係 | — | このデータセットは北海道東部の窓ではなく、世界の標本。ForTy の北海道東部の抽出と同じ名前の主題だが、範囲が別 |
| 不確かな標本 | — | `unsure`・`unresolved` の列で不確かなラベルを区別。全地点には未解決・不確かな記録を含む |
| 版 | — | v0.6 の検証標本（更新されうる） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/forest-typology-validation-2020 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/forest-typology-validation-2020?blobs=true`）と Parquet フッターの取得（2026-10-26）
