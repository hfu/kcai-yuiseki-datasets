---
id: osm-japan-src-2026-08
title: osm-japan-src-2026-08 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/osm-japan-src-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 9a9b4a7、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-tokyo23-src-2026-08
  - geo-triples-japan
dataset: yuiseki/osm-japan-src-2026-08
verified_how: read-data
pattern: questions
finding:
  - 全国のOSM凍結 pbf(2.8GB)と osm2pgsql 形式の Parquet 4表(点・線・面ほか)
---

## 要点

- 全国のOSM凍結 pbf(2.8GB)と osm2pgsql 形式の Parquet 4表(点・線・面ほか)。面は約3,328万。再構築に必要なものも併置。
- 分類: OSM とその派生。元の情報源: OSM planet 2026-08-31 の日本の切り出し。
- 権利: ODbL。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 9a9b4a7（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 9.26 GB、ファイル 12 本 |
| Parquet | 4 本、合計 6.46 GB、最大 4.19 GB |
| 行数 | 50,023,969（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/planet_osm_polygon.parquet`） | 74（うち文字列 59） |
| 行グループ数（標本の最大） | 204 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `addr:housename` 100.0%、`aerialway` 100.0%、`barrier` 100.0%、`bridge` 100.0% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- OSMの日付固定の再現可能な問い
- 道路・建物・POI の全国集計

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet 1.1、Hilbert 曲線順に整列、`bbox` 列つき。行グループ204で範囲読みが効く構造 | — |
| 固定 | 単一ファイルに checksum。読む道具の版も固定 | — |
| 座標系 | — | 幾何は EPSG:3857(Webメルカトル)。1mが緯度で違う(沖縄26°Nで約1.11m、稚内45°Nで約1.41m)。面積は北ほど過大で、全国ランキングは順位が変わりうる。測地系の計算をしない |
| タグ | — | `tags` は hstore でなく JSON 文字列 |
| 重さ | — | 面の表が約4.2GB(1ファイル) |
| 継承 | — | ODbL |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 多重ポリゴンの複数行への分かれ方などはカード参照

## 出典

- yuiseki/osm-japan-src-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/osm-japan-src-2026-08?blobs=true`）と Parquet フッターの取得（2026-10-24）
