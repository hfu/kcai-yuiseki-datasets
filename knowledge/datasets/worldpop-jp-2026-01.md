---
id: worldpop-jp-2026-01
title: worldpop-jp-2026-01 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/worldpop-jp-2026-01 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット cb54e59、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - estat-census-mesh-2020
  - mlit-1km-fromto-2022-01
dataset: yuiseki/worldpop-jp-2026-01
verified_how: read-data
pattern: questions
finding:
  - 100m・1km のセルごとの人口、1kmの性別5歳階級、都市化度
---

## 要点

- 100m・1km のセルごとの人口、1kmの性別5歳階級、都市化度。元 GeoTIFF 1,024本と COG。Parquet は一覧(files)の1本のみ。
- 分類: 世界の地理。元の情報源: WorldPop R2025A 日本(2015〜2030年)。
- 権利: CC BY 4.0(各プロダクトの DOI を引用)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット cb54e59（最終更新 2026-10-02、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 8.42 GB、ファイル 2053 本 |
| Parquet | 1 本、合計 0.1 MB、最大 0.1 MB |
| 行数 | 1,024（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/files.parquet`） | 23（うち文字列 13） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `level` 96.9% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: files.parquet。他のファイルは未検査） |

## 答えうる問い

- 格子人口の将来推計
- 都市化度と人口の関係

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 形式 | COG は範囲読みに向く | — |
| 表の道具では読めない | — | 本体は ラスタ(tif 2,048本、約8.4GB)。Parquet は一覧 |
| 推計 | — | 統計ではなくモデル推計で、2025年以降は予測 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- COG の overview 構成は未確認

## 出典

- yuiseki/worldpop-jp-2026-01 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/worldpop-jp-2026-01?blobs=true`）と Parquet フッターの取得（2026-10-24）
