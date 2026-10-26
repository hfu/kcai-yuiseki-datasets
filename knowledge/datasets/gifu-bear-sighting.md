---
id: gifu-bear-sighting
title: gifu-bear-sighting で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/gifu-bear-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット b7f5947、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - akita-kumadas-wildlife-sighting
  - ishikawa-bear-incident
  - kyoto-bear-sighting
dataset: yuiseki/gifu-bear-sighting
verified_how: read-data
pattern: questions
finding:
  - ツキノワグマの目撃記録6,946件（FY2014〜FY2025）を年度ごと12表の GeoParquet にしたもの
---

## 要点

- ツキノワグマの目撃記録6,946件（FY2014〜FY2025）を年度ごと12表の GeoParquet にしたもの。元の Shapefile の zip（11本）と CSV（1本）も併置。
- 分類: クマ出没記録。元の情報源: 岐阜県「クママップ（過去）」（岐阜県オープンデータカタログ、環境生活政策課）。
- 権利: 元は CC BY 2.1 日本。このデータセットは CC BY 4.0 として提供（同系統の新しい版）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット b7f5947（最終更新 2026-10-26、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 1.2 MB、ファイル 31 本 |
| Parquet | 12 本、合計 0.5 MB、最大 0.1 MB |
| 行数 | 6,946（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/h26.parquet`） | 21（うち文字列 18） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: h26.parquet。他のファイルは未検査） |

## 答えうる問い

- 岐阜県のクマ目撃の年度別・市町村別の件数と場所

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | 元の `.dbf`・`.shp`・CSV を別の読み方で全行・全列照合したとカードが述べる | — |
| 文字 | 全角の数字・英字（`１１月`、`Ｃ-137`）を元のまま保持 | — |
| 12表 | — | 列が年度ごとに違う（Shapefile の項目名は10文字で切れ、`出没時間（` のように途切れる）。1つの表にまとめられていない |
| 座標系 | — | H26〜H30は WGS 84、R1は JGD2011、R2〜R7は平面直角座標（メートル）で `.prj` が無い。カードは「第VII系（EPSG:6675）」と推定して投影した（元は示さない）。R2〜R7の3,236点のうち3,228点が記録の市町村内に入る |
| 意味 | — | 報告であり、同じ個体が複数回報告されうる |
| 個人情報 | — | 入力者（担当職員）の氏名の列を Parquet から除いた（原本の zip には残る） |
| 範囲 | — | 最新の情報は県の GIS にあり、このデータセットには無い。年度が追加されうる |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/gifu-bear-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/gifu-bear-sighting?blobs=true`）と Parquet フッターの取得（2026-10-26）
