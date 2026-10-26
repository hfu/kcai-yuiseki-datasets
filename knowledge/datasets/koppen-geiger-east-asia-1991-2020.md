---
id: koppen-geiger-east-asia-1991-2020
title: koppen-geiger-east-asia-1991-2020 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/koppen-geiger-east-asia-1991-2020 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 0eaf521、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - agera5-japan-monthly-temperature-1979-2026
dataset: yuiseki/koppen-geiger-east-asia-1991-2020
verified_how: read-data
pattern: questions
finding:
  - ケッペン・ガイガーの気候区分図を、同じクラスが4連結で続く領域の多角形（13,480件）にした GeoParquet
---

## 要点

- ケッペン・ガイガーの気候区分図を、同じクラスが4連結で続く領域の多角形（13,480件）にした GeoParquet。クラスコード・記号・説明つき。元の1km ラスタも併置。
- 分類: 気候。元の情報源: Beck et al. (2023) の1km ケッペン・ガイガー図（1991〜2020年、v2）の東アジア窓（122〜154°E、20〜48°N）。
- 権利: CC BY 4.0。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 0eaf521（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 13.5 MB、ファイル 9 本 |
| Parquet | 1 本、合計 1.0 MB、最大 1.0 MB |
| 行数 | 13,480（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/koppen_geiger_east_asia_1991_2020.parquet`） | 5（うち文字列 2） |
| 行グループ数（標本の最大） | 3 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: koppen_geiger_east_asia_1991_2020.parquet。他のファイルは未検査） |

## 答えうる問い

- 日本周辺の気候区分の面的な分布

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | ラスタとの往復の一致を `profile.json` に記録 | — |
| 幾何 | GeoParquet、EPSG:4326 | — |
| 意味 | — | 気候区分の図で、気候の観測値そのものではない。対象期間は1991〜2020 |
| 形 | — | 領域は元の画素の境界を保つ（滑らかでない） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/koppen-geiger-east-asia-1991-2020 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/koppen-geiger-east-asia-1991-2020?blobs=true`）と Parquet フッターの取得（2026-10-26）
