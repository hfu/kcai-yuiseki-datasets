---
id: npa-traffic-accidents
title: npa-traffic-accidents で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/npa-traffic-accidents のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 389500a、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - jp-admin-2026-09
dataset: yuiseki/npa-traffic-accidents
verified_how: read-data
pattern: questions
finding:
  - 人身事故1件=1行(本票)と補充票・高速票
---

## 要点

- 人身事故1件=1行(本票)と補充票・高速票。年1回、年間約30万件。Parquet は年×票ごと21本。
- 分類: 日本の統計・公的GIS。元の情報源: 警察庁「交通事故統計情報のオープンデータ」(2019〜2025年)。
- 権利: PDL1.0(CC BY 4.0 互換)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 389500a（最終更新 2026-10-01、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 579.1 MB、ファイル 76 本 |
| Parquet | 21 本、合計 110.4 MB、最大 18.1 MB |
| 行数 | 2,684,391（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/2019/honhyo.parquet`） | 61（うち文字列 58） |
| 行グループ数（標本の最大） | 4 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 事故の時間・天候・道路形状・当事者の分布
- 都道府県・警察署ごとの傾向

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| キー | 事故は 都道府県コード+警察署等コード+本票番号 で一意。全列が文字列なので先頭のゼロが保たれる | — |
| 幾何 | 10進の緯度経度から点を作ってあり、GeoParquet | — |
| コード | — | 都道府県コードは警察独自で JIS ではない(東京は 13 でなく 30、北海道は5コード)。市区町村データと結合するときは変換表が要る |
| 列の変化 | — | 2022年に列が変わった(本票 58→68列)。年をまたぐ結合は列名で合わせる |
| 型 | — | 全列が文字列。数値は利用側で変換 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 警察署コードと市区町村の対応表は未確認

## 出典

- yuiseki/npa-traffic-accidents のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/npa-traffic-accidents?blobs=true`）と Parquet フッターの取得（2026-10-24）
