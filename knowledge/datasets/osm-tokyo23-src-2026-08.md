---
id: osm-tokyo23-src-2026-08
title: osm-tokyo23-src-2026-08 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/osm-tokyo23-src-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 38f7a5f、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-japan-src-2026-08
  - osm-tokyo23-qa-2026-08
  - osm-tokyo23-questions
dataset: yuiseki/osm-tokyo23-src-2026-08
verified_how: read-data
pattern: questions
finding:
  - 23区のOSM凍結 pbf と osm2pgsql 形式の Parquet 4表(点30.7万、面143.7万)
---

## 要点

- 23区のOSM凍結 pbf と osm2pgsql 形式の Parquet 4表(点30.7万、面143.7万)。osm-japan-src の小さい版。
- 分類: OSM とその派生。元の情報源: OSM planet 2026-08-31 の東京23区の切り出し。
- 権利: ODbL。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 38f7a5f（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 295.3 MB、ファイル 12 本 |
| Parquet | 4 本、合計 207.7 MB、最大 151.1 MB |
| 行数 | 2,124,595（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/planet_osm_polygon.parquet`） | 74（うち文字列 59） |
| 行グループ数（標本の最大） | 71 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `addr:housename` 100.0%、`aerialway` 100.0%、`bridge` 100.0%、`denomination` 100.0% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: planet_osm_line.parquet、planet_osm_roads.parquet。他のファイルは未検査） |

## 答えうる問い

- 23区についての再現可能な地理の問い(215問に対応)

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet 1.1、Hilbert 順、`bbox` 列つき | — |
| 境界 | 境界は同じスナップショットから作る(一年古い境界だと世田谷の環が閉じず Overpass が面を作らない事例が出た) | — |
| 座標系 | — | EPSG:3857。面積・距離はそのまま使えない |
| 範囲 | — | complete_ways のため、箱は東京の外(小笠原航路)まで広がる |
| 継承 | — | ODbL |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/osm-tokyo23-src-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/osm-tokyo23-src-2026-08?blobs=true`）と Parquet フッターの取得（2026-10-24）
