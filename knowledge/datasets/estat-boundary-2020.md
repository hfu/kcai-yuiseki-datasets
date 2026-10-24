---
id: estat-boundary-2020
title: 国勢調査の小地域境界（2020）は、人口を結ぶための基盤になるか
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/estat-boundary/README.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - estat-boundary-2020-duplicate-boundaries
  - jp-admin-2026-09
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-scale
  - yuiseki-datasets-terrio-usage-possibilities
verified_how: read-card
pattern: questions
finding:
  - 小地域境界は「人口の表」と「境界の面」を一緒に持つので、地理結合の基盤として使いやすい
---

## 要点

- このデータセットが答えうる問いの本体は、「どの小地域にどの人口があるか」「どの形を持つか」「どこまで同じ境界か」を扱うこと。
- ただし、人口の集計値は国勢調査の表全体ではなく、境界データの属性の一部に限られるので、単独では年齢別・世帯構成・就業の問いには弱い。
- 行政区域との結合や、他の統計テーブルとの結合に向く。
- 複数行が同じ KEY_CODE を持つ仕様を前提にしないと、人口の合計がずれる。

## 答えうる問いの例

- 小地域ごとの人口と世帯数を、行政区域コードと結びつけて表にする
- どの小地域が「面積最大の境界」かを見つける
- 市区町村ごとの境界の重なりや分割を確認する

## 答えられそうで答えられない問い

- 小地域ごとの全ての属性を、国勢調査統計表のように完全に再現することは難しい
- 町丁・字等境界の定義と、統計表の集計単位が完全に一致しない場合がある

## つまずきやすいところ

- 重複境界の扱い
- `KEY_CODE` と `PREF + CITY + S_AREA` の違い
- `HCODE` による「町丁・字等」と「水面調査区」の違い

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

確かめた版: yuiseki/estat-boundary-2020 のコミット 823195c（2026-09-26）。terrio 0.4.2、duckdb。確かめた県は香川（r2ka37）と東京（r2ka13）。

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | Parquet の日本語属性（`香川県`、`坂出市`）は UTF-8 で正しく読める（terrio で GeoJSON に変換して確認）。元の Shapefile は cp932 だが、Parquet を使えば cp932 の問題を避けられる | 元の Shapefile zip を terrio 0.4.2 で読むと属性が化けた（`.cpg` 無し。参考の 1 回のみ。今は追試しない） |
| 型 | 数値に見える列（JINKO、AREA、CITY）が全部文字列なので、ゼロ落ちや桁落ちは起きない | 計算には CAST が要る。型推論で数値にすると CITY の 3 桁（`402`）が壊れる |
| 幾何の持ち方 | 東京は 6,021 行すべて POLYGON、WKB で読める（カード）。範囲は沖ノ鳥島・南鳥島を含む | GeoParquet の `geo` メタデータが無く、列は素の BLOB。terrio 0.4.2 は `Geometry: None` と見て、変換すると幾何が全部 null になる。CRS もファイルに無い |
| 座標系 | カードと provenance.yaml は JGD2000（EPSG:4612）としている | ファイルからは確かめられない。定義書は「属性情報は JGD2000」、複数の系にまたがる 4 都道県は平面直角座標系の系を決めて書くとある |
| 規模 | 1 県 1 ファイル（2.7〜18.1 MB）。必要な県だけ取れる | 行グループが 1 つ。リモートから読むと、terrio CLI は 4.5 MB の県を全量取得した。1 行あたりの形が大きく、範囲で絞る手段が無い |
| 重複行 | 定義書どおりの仕様で、人口の合計は公表値と一致する | 小地域を 1 行にするには E1/M の解釈が要る。詳しくは `estat-boundary-2020-duplicate-boundaries` |
| キー | KEY_CODE は結合に使える | 長さが 2・9・11 桁と混在。11 桁の PREF+CITY+S_AREA を自分で作る |

- 要約: 属性の読み取りは問題ない（UTF-8、全て文字列）。幾何を GIS の道具にそのまま渡す段階には問題がある（`geo` メタデータ無し）。
- 手元のコピーに `geo` メタデータを足すと、terrio 0.4.2 は幾何を読めた（2026-10-24、香川と東京）。ただし `crs` を書かないと EPSG:4326 とみなされる。さらに `bbox` 列と空間順の行グループを足すと、terrio-js でのリモート読みが 6.9MB のうち 1.3MB（経度順）、Hilbert 順で 100〜250 行/群なら 0.66〜0.74MB（9〜11%）で済んだ（terrio CLI は全量）。詳細は `checks/check-2026-10-24-estat-boundary-geoparquet.md`。元のデータセットは変更していない。

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/estat-boundary/README.md（コミット 6880b32）
