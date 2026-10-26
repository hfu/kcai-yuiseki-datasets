---
id: forty-hokkaido-east-2020
title: forty-hokkaido-east-2020 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/forty-hokkaido-east-2020 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 7247d81、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - forest-typology-validation-2020
  - ctrees-agb-hokkaido-east-100m
dataset: yuiseki/forty-hokkaido-east-2020
verified_how: read-data
pattern: questions
finding:
  - 6クラスの森林タイプ図（10m）の、東部北海道の6タイルを多角形化した GeoParquet（63,630件）
---

## 要点

- 6クラスの森林タイプ図（10m）の、東部北海道の6タイルを多角形化した GeoParquet（63,630件）。元の GeoTIFF のタイル zip も併置。
- 分類: 北海道東部の窓抽出。元の情報源: ForTy v1 2020 森林タイプ図（Figshare+、6クラス、10m）の東部北海道の6タイル。
- 権利: CC BY 4.0（出典の DOI を示す）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 7247d81（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 20.5 MB、ファイル 15 本 |
| Parquet | 1 本、合計 12.8 MB、最大 12.8 MB |
| 行数 | 63,630（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/parquet/forty_east_hokkaido_2020.parquet`） | 4（うち文字列 1） |
| 行グループ数（標本の最大） | 11 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: forty_east_hokkaido_2020.parquet。他のファイルは未検査） |

## 答えうる問い

- 東部北海道の森林タイプ（クラス）の分布と面積

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet。クラスコードを保持（`class_code`・`class_name`） | — |
| 再現性 | `source/raster_55T.zip`（元タイル）、`MANIFEST.json`（SHA-256）、スクリプトを同梱 | — |
| 意味 | — | モデルによる森林・土地利用の類型で、2020は基準年を示し、全入力の観測日ではない。この抽出は独立した現地検証ではない（カード） |
| 形 | — | 境界は10m画素に従って非常に細かい。個々の画素を現地確認済みの境界として読まない |
| 件数 | — | ソース70,026,240セルのうち分類済み68,700,160、NoData 1,326,080（カード） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/forty-hokkaido-east-2020 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/forty-hokkaido-east-2020?blobs=true`）と Parquet フッターの取得（2026-10-26）
