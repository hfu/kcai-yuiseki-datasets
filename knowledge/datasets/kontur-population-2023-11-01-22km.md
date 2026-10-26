---
id: kontur-population-2023-11-01-22km
title: kontur-population-2023-11-01-22km で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/kontur-population-2023-11-01-22km のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 2e7291f、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - ghsl-japan-core-2020-30arcsec
dataset: yuiseki/kontur-population-2023-11-01-22km
verified_how: read-data
pattern: questions
finding:
  - 世界を H3 解像度4（約22km）のセルにした人口の推定（71,283セル）
---

## 要点

- 世界を H3 解像度4（約22km）のセルにした人口の推定（71,283セル）。多角形と多角形群を含む GeoParquet。元の GeoPackage gzip も併置。
- 分類: 人口・建物・土地被覆。元の情報源: Kontur Population 2023-11-01 の世界22km H3 格子（HDX）。
- 権利: Hugging Face のタグは other（CC BY。HDX の記載）。「Kontur Population dataset © Kontur」の表示が必要。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 2e7291f（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 10.2 MB、ファイル 7 本 |
| Parquet | 1 本、合計 3.5 MB、最大 3.5 MB |
| 行数 | 71,283（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/kontur_population_20231101_r4.parquet`） | 4（うち文字列 1） |
| 行グループ数（標本の最大） | 7 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: kontur_population_20231101_r4.parquet。他のファイルは未検査） |

## 答えうる問い

- 世界の人口分布の粗い比較
- H3 セルによる集計の起点

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| キー | `h3` は一意 | — |
| 座標系 | 元は EPSG:3857 のまま保持（カード） | EPSG:3857 で面積・距離がそのまま使えない |
| 粗さ | — | 22km 格子で、日本国内の小地域の問いには粗い |
| 時点 | — | 2023-11-01で凍結 |
| 範囲読み(実測) | — | 幾何の CRS は EPSG:3857。経緯度の bbox だと0件。3857の bbox（9セル）でも 3.5MB（全体）を読んだ |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/kontur-population-2023-11-01-22km のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/kontur-population-2023-11-01-22km?blobs=true`）と Parquet フッターの取得（2026-10-26）
