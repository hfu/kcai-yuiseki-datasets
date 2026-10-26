---
id: worldpop-kor-population-2015-2030-1km-r2025a
title: worldpop-kor-population-2015-2030-1km-r2025a で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/worldpop-kor-population-2015-2030-1km-r2025a のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット d22e0e7、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - worldpop-idn-population-2015-2030-1km-r2025a
  - worldpop-jp-2026-01
dataset: yuiseki/worldpop-kor-population-2015-2030-1km-r2025a
verified_how: read-data
pattern: questions
finding:
  - WorldPop の2015〜2030年の年次人口推定を、韓国の1km 格子のセル多角形にした GeoParquet（130,927セル
---

## 要点

- WorldPop の2015〜2030年の年次人口推定を、韓国の1km 格子のセル多角形にした GeoParquet（130,927セル。全年でNoDataの371,433セルは省略）。
- 分類: 人口・建物・土地被覆。元の情報源: WorldPop R2025A v1 韓国の年次人口（STAC、1km）。
- 権利: Hugging Face のタグは other（メタデータ名は odbl-1.0-worldpop-cc-by-4.0-source）。LICENSE に ODbL 1.0 を保守的な選択として採った理由を書く（内容は読んでいない）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d22e0e7（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 12.9 MB、ファイル 5 本 |
| Parquet | 1 本、合計 12.9 MB、最大 12.9 MB |
| 行数 | 130,927（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/population.parquet`） | 19（うち文字列 0） |
| 行グループ数（標本の最大） | 11 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 文字の検査 | 文字列の列が無い（検査不要） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: population.parquet。他のファイルは未検査） |

## 答えうる問い

- 韓国の人口分布の推移と将来推計（モデル）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| キー・型 | `(grid_row, grid_col)` は一意。NoData は null、数値の0は0として保持 | — |
| 再現性 | STAC のアイテム ID、SHA-256、全年の画素値の照合結果（`VERIFICATION.json`）を同梱 | — |
| 意味 | — | モデルの推定（dasymetric）で、セルごとの国勢調査の値ではない。1kmの格子が入力の精度を意味しない。R2025A は alpha リリースで更新されうる |
| 欠測 | — | 全年でNoDataの371,433セルは省略。年ごとのNoDataは `-99999` がnullになり、数値の0は0のまま |
| 格子 | — | 760×661、30秒の角度格子で等積でない |
| 原本 | — | 元のラスタは再配布していない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/worldpop-kor-population-2015-2030-1km-r2025a のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/worldpop-kor-population-2015-2030-1km-r2025a?blobs=true`）と Parquet フッターの取得（2026-10-26）
