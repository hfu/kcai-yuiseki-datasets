---
id: gpw-grasslands-hokkaido-east-2018-2020-250m
title: gpw-grasslands-hokkaido-east-2018-2020-250m で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/gpw-grasslands-hokkaido-east-2018-2020-250m のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 92c36ce、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - ctrees-agb-hokkaido-east-100m
  - forty-hokkaido-east-2020
dataset: yuiseki/gpw-grasslands-hokkaido-east-2018-2020-250m
verified_how: read-data
pattern: questions
finding:
  - 草地の優占クラス（耕作草地・自然半自然草地・低木地・その他）の30m図を、10×10画素のブロック（約250m）に集約した多角形（313,489件）
---

## 要点

- 草地の優占クラス（耕作草地・自然半自然草地・低木地・その他）の30m図を、10×10画素のブロック（約250m）に集約した多角形（313,489件）。3年分のクラス別画素数と優占クラスを持つ。
- 分類: 北海道東部の窓抽出。元の情報源: Global Pasture Watch の草地クラス図（Zenodo v2-beta、2018〜2020年）の東部北海道。
- 権利: CC BY 4.0（出典は Parente et al. 2025、Zenodo 15648551）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 92c36ce（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 13.3 MB、ファイル 9 本 |
| Parquet | 1 本、合計 4.8 MB、最大 4.8 MB |
| 行数 | 313,489（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/grassland_class_2018_2020.parquet`） | 21（うち文字列 0） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 文字の検査 | 文字列の列が無い（検査不要） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: grassland_class_2018_2020.parquet。他のファイルは未検査） |

## 答えうる問い

- 東部北海道の草地の種類の分布と、2018〜2020年の変化

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet 1.1.0、EPSG:4326 | — |
| 再現性 | 元の COG の窓（3年分）、`SOURCES.json`・`MANIFEST.json`（MD5・SHA-256）を同梱 | — |
| 意味 | — | モデルの分類で、現地の真値ではない。約250mのセルは30m分類の集約で、その解像度での新しい予測ではない。変化を土地利用の測定された変化として読まない |
| 範囲 | — | 2018〜2020年の3年分で、親レコードの題名（2000〜2024年）の2024年の図ではない |
| 窓 | — | 要求した範囲（142〜144°E）と、実際の範囲（141.9995〜143.9995°E）が、格子に合わせて少しずれる |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/gpw-grasslands-hokkaido-east-2018-2020-250m のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/gpw-grasslands-hokkaido-east-2018-2020-250m?blobs=true`）と Parquet フッターの取得（2026-10-26）
