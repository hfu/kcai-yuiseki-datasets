---
id: usgs-comcat-2025-m45
title: usgs-comcat-2025-m45 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/usgs-comcat-2025-m45 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 028c1c8、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - ibtracs-v04r01
dataset: yuiseki/usgs-comcat-2025-m45
verified_how: read-data
pattern: questions
finding:
  - 2025年のマグニチュード4.5以上の地震8,502件（優先ネットワーク `us`、事象種別 earthquake）
---

## 要点

- 2025年のマグニチュード4.5以上の地震8,502件（優先ネットワーク `us`、事象種別 earthquake）。クエリは8,558件を返し、他ネットワークと非地震1件を除いた（マニフェストに数を記録）。
- 分類: 災害・気象。元の情報源: USGS ComCat 2025年 M4.5以上（preferred network `us`）。
- 権利: Hugging Face のタグは other（USGS）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 028c1c8（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 6.7 MB、ファイル 8 本 |
| Parquet | 1 本、合計 0.6 MB、最大 0.6 MB |
| 行数 | 8,502（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/earthquakes.parquet`） | 29（うち文字列 15） |
| 行グループ数（標本の最大） | 5 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `tz` 100.0%、`alert` 91.2%、`mmi` 90.1%、`felt` 84.0% |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: earthquakes.parquet。他のファイルは未検査） |

## 答えうる問い

- 2025年の世界の大きな地震の分布
- 日本周辺の地震の件数（M4.5以上）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 件数 | クエリ結果と除外件数をマニフェストに記録 | — |
| 幾何 | 点の GeoParquet（CRS は未記載。既定の WGS 84） | — |
| 範囲 | — | マグニチュードの閾値と優先ネットワークで絞った標本で、検知力が均一でない完全な目録ではない。無い事象は「地震活動が無い」を意味しない |
| 時点 | — | ComCat は改訂されうる。取得時点の1つの状態 |
| 範囲外 | — | マグニチュード4.5未満、他の優先ネットワークの事象は無い |
| 欠損(実測) | — | `tz` は全行null、`felt`（有感報告）は84%、`mmi` は90%がnull |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/usgs-comcat-2025-m45 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/usgs-comcat-2025-m45?blobs=true`）と Parquet フッターの取得（2026-10-26）
