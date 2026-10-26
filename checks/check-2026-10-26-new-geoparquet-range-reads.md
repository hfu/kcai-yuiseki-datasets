# 新規の GeoParquet に対する terrio-js の範囲読み（2026-10-26）

環境: Claude Code クラウドセッション、npm の terrio-js 0.4.2（Node 22）。配信は Hugging Face の `resolve/main/…`（CDN に転送）。`openUrl` のあと `read({bbox})`、`stats()` の `bytes`（受信量）と `requests`。窓は各データセット内の小さな範囲（0.05〜0.1 度四方など）。

## 結果

| データセット（ファイル） | 窓の地物数 | 受信量 / ファイル | 要求数 | 行グループ |
|---|---|---|---|---|
| gfw-forest-carbon-net-flux（net_flux） | 136,081 | 27.1MB / 36.8MB（約73%） | 29 | 47 |
| worldpop-idn（population） | 169 | 13.4MB / 94.2MB（約14%） | 35 | 33 |
| gebco（elevation） | 25 | 3.91MB / 3.90MB（全量） | 3 | 17 |
| esa-worldcover（100m） | 3,844 | 4.69MB / 4.72MB（全量） | 3 | 8 |
| ghsl（R6_C32 人口） | 169 | 16.07MB / 16.3MB（全量） | 6 | 15 |
| ibtracs | 982 | 8.78MB / 8.69MB（全量） | 16 | 7 |
| usgs-comcat | 243 | 0.57MB（全量） | 3 | 5 |
| ksj-a31a-flood（flood_area） | 2,852 | 106.6MB（全量） | 10 | 5 |
| microsoft-building-footprints（QuadKey 133002112、渋谷） | 5,657 | 273.2MB / 273.2MB（全量） | 4 | 392 |
| forty（UTM 55N の bbox） | 226 | 12.75MB（ほぼ全量） | 3 | 11 |
| kontur（EPSG:3857 の bbox） | 9 | 3.54MB（全量） | 4 | 7 |

- **経緯度の窓が使えない例**: forty（CRS は UTM 55N）と kontur（EPSG:3857）は、経緯度の bbox で読むと**0件**が返る（エラーは出ない）。bbox は幾何の CRS の座標で与える。
- microsoft-building-footprints の QuadKey 133002113 は経度 139.92〜140.62°・緯度 35.46〜36.03° の範囲で、渋谷付近や筑波付近の窓は 0 件（範囲外）。
- 行グループが多くても、飛ばせるとは限らない（microsoft-building-footprints は 392 行グループで全量）。
- 部分的に飛ばせたのは、gfw（73%）と worldpop-idn（14%）。どの統計が使われたかは確認していない。gfw の `geometry` 列には統計がある（duckdb で確認）。worldpop-idn は `grid_row`・`grid_col` などに統計がある。いずれも bbox の covering 列は無い。

## 限界

- 窓は各1つ。窓の取り方で結果は変わる（estat-boundary-2020 の実験では窓ごとに差が大きかった）。
- 配信は Hugging Face の CDN。要求数と所要時間は回線による。
- terrio-js 0.4.2 のみ。terrio CLI（全量取得）、DuckDB は測っていない。
