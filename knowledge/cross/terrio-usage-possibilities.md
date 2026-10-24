---
id: yuiseki-datasets-terrio-usage-possibilities
title: terrio で yuiseki-datasets を活用する可能性：読める形、落とし穴、組み合わせ方
status: draft
sources:
  - dwg7/kcai-terrio knowledge/cloud-native-read-behavior-matrix.md（terrio 0.3.2、2026-10-21）
  - dwg7/kcai-terrio knowledge/shapefile-cp932-attributes-not-decoded.md（terrio 0.3.2、2026-10-21）
  - dwg7/kcai-terrio knowledge/terrio-formats-vectors-streaming-and-tiles.md（terrio 0.3.2、2026-10-21）
  - dwg7/kcai-terrio AGENTS.md、README.md
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md、jp-admin-2026-09.md、README.md（コミット 6880b32）
  - 2026-10-24 の実測（terrio 0.4.2、PyPI の wheel、Linux x86_64）。手順は checks/check-2026-10-24-terrio-reads.md、checks/check-2026-10-24-estat-boundary-geoparquet.md
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-categories
  - yuiseki-datasets-japan-admin-lineage
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-scale
  - estat-boundary-2020
  - jp-admin-2026-09
verified_how: read-data
pattern: pattern
finding:
  - Hugging Face 上の Parquet を使えば Shapefile（cp932）は避けられる。ただし terrio 0.4.2 は、GeoParquet メタデータの無い estat-boundary-2020 の幾何を読めず（Geometry None）、メタデータのある jp-admin-2026-09 HEAD は問題なく読めた。Shapefile を避けられるかは、データセットの Parquet が GeoParquet として作られているかで決まる
---

## 要点

- kcai-terrio は「クラウドネイティブなデータをクラウドネイティブに触る」遊びの場で、範囲読み込み（HTTP Range）を重視し、日本ローカル（JGD2011、平面直角座標、日本語属性）を試している。yuiseki-datasets は、Hugging Face 上の Parquet（URL 固定で Range に応える）と、日本の公的データの派生物が多く、相性のよい試験場になる。
- ただし、いま実測できた範囲では、estat-boundary-2020 は terrio にそのまま渡して使える形ではない（下表）。
- 以下の「可能性」の節は仮説。実測した事実は「確かめたこと」の節に分けた。

## 確かめたこと（2026-10-24、terrio 0.4.2、手元で実行）

| 入力 | 操作 | 結果 |
|---|---|---|
| estat-boundary-2020 `parquet/r2ka37.parquet`（香川、1,010 行、4,520,782 バイト） | `terrio info` | `Driver: Parquet`、`Geometry: None`、`CRS: unknown`、`geometry: Blob`。属性は全部 Text |
| 同上 | `terrio convert` → GeoJSON | 1,010 地物。**全地物の geometry が null**。属性の日本語（香川県、坂出市）は正しい |
| 同 URL（Hugging Face） | `TERRIO_HTTP_LOG=YES terrio info` | 先頭 64 KiB を Range で 206 → 続けて全体を GET（302 から CDN 200）し 4,520,782 バイト受信。**範囲読みにならず全量取得** |
| 同じデータの元 Shapefile（香川の zip を展開）【参考の 1 回だけ。追試はしない】 | `terrio info` / `convert` | 幾何は Polygon、CRS は `EPSG:4612 (JGD2000)`。**属性が化ける**（PREF_NAME `香川県` が `ì§` のような文字列に）。zip に `.cpg` は無い |
| jp-admin-2026-09 municipalities（HEAD e6c87b1、148.6 MB、ローカル） | `terrio info` / `convert --where "pref_code = '37'"` | `MultiPolygon`、1,918、`EPSG:4612`。17 地物の GeoJSON が出て、`name` `高松市`、`pref` `香川県`、`lg_code` `372013` が正しい |

- Parquet 側の原因は、Yuiseki さんのカードの記述と整合する: 幾何は WKB の BLOB で、GeoParquet の `geo` メタデータが無い。terrio がそれを幾何として認識しないと見える（terrio 側の仕様は未確認）。
- 元 Shapefile の文字化けは、kcai-terrio の `shapefile-cp932-attributes-not-decoded`（0.3.2）と同じ現象が 0.4.2 でも起きた、という参考の観察にとどめる。
## メタデータを足した結果（estat-boundary-2020 のコピー、2026-10-24）

手順と数は `checks/check-2026-10-24-estat-boundary-geoparquet.md`。

- `geo` メタデータ（WKB、Polygon、bbox）を足すと、terrio CLI は `Polygon`、1,010 件、幾何も読めた。範囲は元 Shapefile のものと一致。
- **CRS を書かないと EPSG:4326 とみなされる**。JGD2000 のデータが WGS 84 と表示される。`crs` に EPSG:4612 を書くと `EPSG:4612 (JGD2000)` になった。
- `--spat` の結果（渋谷周辺 55 地物）は shapely の交差判定と一致。
- リモート（ローカルの Range サーバー）の読み: terrio CLI は全量取得（メタデータや bbox 列の有無によらない）。terrio-js は、`bbox` 列と空間順の行グループがあるとき 6.9MB のうち 1.3MB（約19%）で同じ 55 地物を返し、`geo` メタデータだけ（行グループの bbox が無い）の変種は全量（6.4MB）だった。
- 未確認: Hugging Face の CDN 経由、47 県全部、terrio 以外の道具。元のデータセットは変更していない。

- 未確認（残り）: リモートの jp-admin を読んだときの転送量。
- 全データセットの `geo` メタデータの有無と置き方は `yuiseki-datasets-access-methods`、規模は `yuiseki-datasets-scale`。

## 可能性（仮説。上の実測以外は未試験）

1. **前処理の検証（2026-10-24 に実施。下の「メタデータを足した結果」）**: estat-boundary-2020 の Parquet に GeoParquet 1.1 のメタデータを足すと、terrio 0.4.2 で幾何が読めた。手本は同じ作者の jp-admin HEAD。kcai-terrio の記録では、terrio は GeoParquet 1.1（covering.bbox 付き）を書き出せる。
2. **範囲読みの比較**: kcai-terrio の記録では、Hugging Face の行グループ 1 つの GeoParquet は WebAssembly 版でもほぼ全体を読んだ。estat-boundary-2020 は都道府県ごと（2.7〜18 MB）に分割されているので、全量でも 1 県単位なら現実的。Yuiseki さんの docs も、形の列が大部分を占め bbox 列が無いと、範囲で絞っても行グループを飛ばせないと測っている。
3. **日本ローカルの試験データ**: jp-admin と abr-src は座標系の混在（abr の代表点は EPSG:4612 と 6668 が混ざる）の試験になる。元の Shapefile（cp932）を経由した試験は、hfu の判断で今は優先しない（terrio が成熟したら、zip のままブラウザから読む試験が望ましい）。
4. **座標変換**: 平面直角座標への変換は、東京（9 系を含む）、北海道（12 系）、沖縄（15 系）など複数の系にまたがる県で試す余地がある。e-Stat の定義書に、この 4 都道県が複数の系にまたがるとの注記がある。
5. **他のデータセット**: natural-earth（GeoParquet、レイヤー別）、gsi-evacuation-sites-jp、mlit-toshi-keikaku-jp などの GeoParquet は、`geo` メタデータの有無で扱いが変わると思われる（未確認）。
6. **逆向き**: terrio で作った結果（変換した GeoParquet）を、`geo-triples-jp-gov` のような派生データの検証に使う。

## 守ること（kcai-terrio の方針から）

- 公開データだけ、大きなデータはリポジトリに入れない、通信先の制限をすり抜けない、外部への投稿は hfu が行う。上流（opengeos/terrio）への報告は下書きにとどめる。
- 版を必ず記録する。上の実測は 0.4.2 で、kcai-terrio の記録は 0.3.2 が中心。版が上がったら確かめ直す。

## 出典

- dwg7/kcai-terrio の上記の踏み跡と AGENTS.md
- yuiseki/study-geoai-algo-py の上記カード（コミット 6880b32）
- checks/check-2026-10-24-terrio-reads.md
