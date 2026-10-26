---
id: esa-worldcover-tokyo-2021-100m
title: esa-worldcover-tokyo-2021-100m で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/esa-worldcover-tokyo-2021-100m のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 6f006f6、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - microsoft-building-footprints-kanto-2026-08-13
  - ghsl-japan-core-2020-30arcsec
dataset: yuiseki/esa-worldcover-tokyo-2021-100m
verified_how: read-data
pattern: questions
finding:
  - 10m の土地被覆図を、10×10画素のブロック（約100m、360,000件）の多角形にし、11クラスの画素数・優占クラス・優占率を持たせた GeoParquet
---

## 要点

- 10m の土地被覆図を、10×10画素のブロック（約100m、360,000件）の多角形にし、11クラスの画素数・優占クラス・優占率を持たせた GeoParquet。
- 分類: 人口・建物・土地被覆。元の情報源: ESA WorldCover 2021 v200（10m、タイル N33E138）の東京周辺の窓（139.5〜140.0°E、35.5〜36.0°N）。
- 権利: CC BY 4.0（© ESA WorldCover project 2021）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 6f006f6（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 34.1 MB、ファイル 17 本 |
| Parquet | 1 本、合計 4.8 MB、最大 4.8 MB |
| 行数 | 360,000（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/parquet/esa_worldcover_tokyo_2021_v200_100m.parquet`） | 19（うち文字列 1） |
| 行グループ数（標本の最大） | 8 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: esa_worldcover_tokyo_2021_v200_100m.parquet。他のファイルは未検査） |

## 答えうる問い

- 東京周辺の土地被覆の構成（100m ブロックごと）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 完全性 | 11クラスと NoData の画素数を持ち、元の10mクラスを1つの値に置き換えない。クラス別の合計 = `valid_pixels` | — |
| 再現性 | 元のタイルと窓の GeoTIFF、`MANIFEST.json`、スクリプト、テストを同梱 | — |
| 範囲 | — | 固定の長方形の窓で、行政区域ではない（東京・埼玉・千葉・神奈川の一部） |
| 集約 | — | 優占クラスだけでは混在が見えない。同数のときは小さいコードを選び、全部NoDataのブロックは0 |
| 時点 | — | 2021年の図（v200） |
| 範囲読み(実測) | — | terrio-js の bbox 読み（0.05°四方、3,844ブロック）で 4.69MB／全体4.72MB（全量） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/esa-worldcover-tokyo-2021-100m のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/esa-worldcover-tokyo-2021-100m?blobs=true`）と Parquet フッターの取得（2026-10-26）
