# estat-boundary-2020 に GeoParquet メタデータを足して terrio で試す（2026-10-24）

## 目的

`yuiseki/estat-boundary-2020`（コミット 823195c）の Parquet は、幾何が素の WKB の BLOB で `geo` メタデータが無い。terrio 0.4.2 は `Geometry: None` と見て、変換すると幾何が全部 null になった。メタデータを足すと何が変わるかを、手元のコピーで確かめた。元のデータセットには何も書いていない。

## 手順

環境: Claude Code クラウドセッション、Linux x86_64、PyPI の terrio 0.4.2、npm の terrio-js 0.4.2（Node 22）、pyarrow 26、shapely。対象は香川（r2ka37、1,010 行）と東京（r2ka13、6,021 行）。

`pyarrow` で元のテーブルを読み、次の3通りに書き直した（行グループは 500 行、zstd）。

| 変種 | 足したもの |
|---|---|
| nocrs | `geo` メタデータ（version 1.1.0、primary_column、encoding WKB、geometry_types、bbox）。CRS なし |
| crs | 上に加えて `crs`（PROJJSON、EPSG:4612 JGD2000） |
| bbox | 上に加えて `bbox` 列（xmin/ymin/xmax/ymax の struct）と `covering.bbox`。行を図形の経度の中心で並べ替え |

CRS は、カードと provenance.yaml の記述（JGD2000 の経緯度）と、e-Stat 定義書の「属性情報は JGD2000」に従った。データの座標が JGD2000 かどうかは、ファイルからは確かめていない。

## 結果

### ローカルで terrio CLI（香川）

| 変種 | `terrio info` | `terrio convert` → GeoJSON |
|---|---|---|
| 元のファイル | `Geometry: None`、`CRS: unknown` | 幾何が全地物 null |
| nocrs | `Polygon`、1,010、**`EPSG:4326 (WGS 84)`** | 幾何 1,010 件すべて Polygon、日本語属性も正しい |
| crs | `Polygon`、1,010、`EPSG:4612 (JGD2000)` | 同上、GeoJSON の crs は EPSG:4612 |
| bbox | 同上 | 同上 |

- 範囲（133.4466,34.0124 – 134.4479,34.5649）は、前回に元 Shapefile から読んだ範囲と小数まで一致した。
- **CRS を書かないと、terrio は EPSG:4326 とみなす**（GeoParquet の既定）。JGD2000 のデータが WGS 84 と表示され、間違いに気づかない。

### 空間フィルタ（東京）

- `terrio convert … --spat 139.69 35.65 139.72 35.67`（渋谷周辺）は 55 地物。shapely で数えた「交差する」件数 55 と一致（箱同士の重なりは 56）。
- 東京の不正な幾何は 4 件（shapely）で、カードの記述と一致。範囲（136.07〜153.98、20.43〜35.90）もカードと一致。

### リモートの範囲読み（東京。ローカルの Range 対応サーバーに置いて測定）

| 入口 | 変種 | 転送量 | 要求数 | 結果 |
|---|---|---|---|---|
| terrio CLI 0.4.2 | crs（6,435,257 B） | 6,435,257 B（全量） | 1 | 55 地物 |
| terrio CLI 0.4.2 | bbox（6,935,392 B） | 6,935,392 B（全量） | 1 | 55 地物 |
| terrio-js 0.4.2（Node） | crs | 6,435,257 B（全量） | 4 | 55 地物。行グループの bbox が null |
| terrio-js 0.4.2（Node） | bbox | **1,299,296 B（約 19%）** | 7 | 55 地物。行グループごとの bbox が見える |

- CLI は `bbox` 付きでも全量取得だった。範囲読みが効いたのは terrio-js のみ。
- 範囲読みの効き目は、`geo` メタデータだけでは出ず、`bbox` 列と、空間的にまとまった行グループが必要だった。
- 行グループの切り方は粗い（経度の中心で並べただけ。最初の行グループは小笠原を含み経度 136〜139.3 度に広がる）。Hilbert 順などにすれば、さらに絞れる可能性がある（未試験）。

## 限界

- 配信は手元のサーバー（Range 対応）。Hugging Face の CDN 経由ではない。CDN での挙動は kcai-terrio の記録（行グループが1つだと全量）と同じ方向と見るが、測っていない。
- 2県のみ。47県全部、北海道（18MB）などは未試験。
- メタデータを足したコピーは手元のみ。Hugging Face のデータセットを変更する提案は、hfu が判断する（このリポジトリからは投稿しない）。
- terrio 以外の道具（DuckDB spatial、GeoPandas、QGIS）での読み取りは未確認。

## 作ったもの

`pyarrow` で `geo` を `schema.metadata` に書き、`bbox` 列を足して行を並べ替え、`row_group_size=500` で書き出す約 30 行のスクリプト（スクラッチに置き、リポジトリには入れていない）。
