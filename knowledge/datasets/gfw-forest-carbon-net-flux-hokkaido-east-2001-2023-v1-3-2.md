---
id: gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2
title: gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 74d3167、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - ctrees-agb-hokkaido-east-100m
  - forty-hokkaido-east-2020
dataset: yuiseki/gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2
verified_how: read-data
pattern: questions
finding:
  - 正味フラックス（2001〜2023年の累積、Mg CO₂e/ha）が0でないセルの中心点を、点の GeoParquet（34,516,630行）にしたもの
---

## 要点

- 正味フラックス（2001〜2023年の累積、Mg CO₂e/ha）が0でないセルの中心点を、点の GeoParquet（34,516,630行）にしたもの。元の10°タイルも併置。
- 分類: 北海道東部の窓抽出。元の情報源: Global Forest Watch の森林炭素の正味フラックス v1.3.2（Harvard Dataverse）の東部北海道（143〜146°E、42〜45°N）。
- 権利: CC0 1.0（Dataverse の記録）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 74d3167（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc0-1.0 |
| 全体 | 127.1 MB、ファイル 10 本 |
| Parquet | 1 本、合計 36.9 MB、最大 36.9 MB |
| 行数 | 34,516,630（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/net_flux.parquet`） | 4（うち文字列 0） |
| 行グループ数（標本の最大） | 47 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 文字の検査 | 文字列の列が無い（検査不要） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: net_flux.parquet。他のファイルは未検査） |

## 答えうる問い

- 東部北海道の森林炭素の吸収源・排出源の分布

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet 1.1、点（セルの中心）。47の行グループがある | — |
| 検証 | `source/VERIFICATION.json`（件数、値の範囲、出力のチェックサム）を同梱 | — |
| 意味 | — | モデル推定。2001〜2023の累積で、年ごとの値として読まない。23で割っても期間平均で、年次の観測ではない |
| 形 | — | 点はセルの中心で、画素の範囲ではない。0でないセルだけなので、「セルが無い」と「0」を区別できない（元の NoData は省略） |
| 規模 | — | 1ファイル3,452万行（約37MB）。リモートの範囲読みには bbox 列が無い |
| 範囲読み(実測) | — | terrio-js 0.4.2 の bbox 読み（0.1°四方、136,081点）は 27.1MB／全体36.8MB（約73%）、29要求。行グループ47のうち一部を統計で飛ばせたが、大半を読んだ。bbox の covering は無い |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2 のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2?blobs=true`）と Parquet フッターの取得（2026-10-26）
