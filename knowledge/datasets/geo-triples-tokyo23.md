---
id: geo-triples-tokyo23
title: geo-triples-tokyo23 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/geo-triples-tokyo23 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 2de36a7、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - geo-triples-japan
  - osm-tokyo23-src-2026-08
dataset: yuiseki/geo-triples-tokyo23
verified_how: read-data
pattern: questions
finding:
  - 東京23区とPOIの空間関係の三つ組(triples 510,616行)、文(cpt 483,922行)、評価問題(probe 8,854行)
---

## 要点

- 東京23区とPOIの空間関係の三つ組(triples 510,616行)、文(cpt 483,922行)、評価問題(probe 8,854行)。
- 分類: OSM とその派生。元の情報源: osm-tokyo23-src-2026-08 と Natural Earth。
- 権利: ODbL-1.0。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 2de36a7（最終更新 2026-09-25、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 8.0 MB、ファイル 9 本 |
| Parquet | 3 本、合計 8.0 MB、最大 5.4 MB |
| 行数 | 1,003,392（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/cpt.parquet`） | 11（うち文字列 11） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: cpt.parquet、probe.parquet。他のファイルは未検査） |

## 答えうる問い

- 23区内のPOIの帰属を答える言語モデルの学習・評価

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 件数 | triples・cpt は実測がカードと一致 | — |
| カード内の食い違い | — | 冒頭は評価問題を8,890、本文は8,854と書く。実測は8,854 |
| 継承 | — | ODbL |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/geo-triples-tokyo23 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/geo-triples-tokyo23?blobs=true`）と Parquet フッターの取得（2026-10-24）
