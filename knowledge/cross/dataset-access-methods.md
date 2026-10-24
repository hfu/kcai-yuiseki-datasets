---
id: yuiseki-datasets-access-methods
title: yuiseki のデータセットへのアクセス方法の対比：置き方、URL、道具ごとの読まれ方
status: draft
sources:
  - Hugging Face API `/api/datasets/<名前>?blobs=true`（2026-10-24。ファイル一覧とサイズ、sha）
  - Parquet のフッター取得（`geo` メタデータの有無。データセットごとに最大の Parquet 1 本）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/README.md の「Parquet を URL から読むときの挙動」（コミット 6880b32）
  - dwg7/kcai-terrio knowledge/cloud-native-read-behavior-matrix.md（terrio 0.3.2、2026-10-21）
  - 2026-10-24 の実測（terrio 0.4.2、duckdb）。checks/check-2026-10-24-terrio-reads.md
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-index
  - yuiseki-datasets-scale
  - yuiseki-datasets-version-policies
  - yuiseki-datasets-terrio-usage-possibilities
  - yuiseki-datasets-categories
verified_how: read-data
pattern: pattern
finding:
  - 「データセットになった時点で GeoParquet がある」とは言えない。2026-10-24 時点で、確認した最大 Parquet に GeoParquet の `geo` メタデータがあるのは 19 件、無いのは 42 件（表やテキストを含む）、Parquet 自体が無いのは 8 件。同じ作者の中でも作りが揃っていく途中にある
---

## 要点

- 共通の入口は `https://huggingface.co/datasets/<名前>/resolve/<コミット>/<パス>`。Yuiseki さんの測定では、Xet の CDN に転送され、Range 要求に 206 で応える。DuckDB は部分取得で読める（ただし読み飛ばせるのは列と行グループの単位まで）。URL にはブランチ名でなくコミットのハッシュを入れて版を固定する。
- 置き方は、規模・形式・版の扱いで 6 つの型に分かれる（下表）。
- 道具によって「Range で読める」の意味が違う。同じ URL でも、DuckDB・terrio CLI・terrio-js で転送量が変わる。

## データセット側の置き方（6 つの型）

| 型 | 中身 | 例 | 使い方の含意 |
|---|---|---|---|
| A 単一の Parquet | `data/train-*.parquet` または 1〜2 本 | osm-wiki、un-docs、wikidata-gazetteer、egov-laws-jp、text2geoql | 全部読む前提。大きいものは 400〜550 MB の 1 本 |
| B 分割した Parquet | 県・レイヤー・表・年ごとに 1 本ずつ | estat-boundary-2020（47 県）、ksj-n07-bus-route-jp（48 県）、nfgis-2024（47 系）、natural-earth（215 レイヤー）、estat-jumin-idou（472 表）、un-wpp（54）、worldbank-wdi（42）、pwt（41） | 必要な単位のファイルだけ取れる。「分割」が Range の代わりに働く |
| C 版ごとのディレクトリ | 日付や版の名前のディレクトリ | geonames（`20261001`）、opencellid（`2026-10-06`）、unhcr-refugee-stats、ekidata-jp、worldbank-wdi（`2026-07-15`）、npa-traffic-accidents（年） | 取得日で中身が変わる。版を明記して引く |
| D 元の配布物を併置 | Parquet と同じ中身の zip、gz、csv、xlsx、dta、geojson、pbf | estat-boundary-2020（Shapefile zip）、abr-src（CSV zip 53）、mlit-toshi-keikaku-jp、gsi-evacuation-sites-jp（geojson） | 検証や再変換に使える。全体では元の配布物が Parquet の約 1.7 倍の量になる |
| E Parquet 無し | zip、gz、jsonl だけ | faostat、ilostat、edgar-ghg-countries、gsj-reports、mlit-river-basin-overviews、moni1000-reports、nilim-disaster-reports、rinya-forest-inventory | 丸ごと落として自分で開く |
| F 非表データ | GeoTIFF、pbf | worldpop-jp-2026-01（tif 2,048 本）、osm-*-src（pbf） | 表の道具では読めない。Parquet は索引や付随表 |

## 地物の形式（Parquet の中の幾何の持ち方）

確認したのは、データセットごとに最大の Parquet 1 本のフッター。`geo`＝GeoParquet のメタデータあり。

- **あり（19 件）**: jp-admin-2026-09（GeoParquet 1.1、MultiPolygon/Polygon、`bbox` covering、CRS は EPSG:4612）、nfgis-2024、osm-japan-src、osm-tokyo23-src（これらも covering あり）、natural-earth、gsi-global-map-jp、mlit-toshi-keikaku-jp、ksj-*（4 件）、geonames、opencellid、ourairports、ucdp-ged、npa-traffic-accidents、ekidata-jp、gsi-evacuation-sites-jp、mlit-underpass。
- **なし**: estat-boundary-2020 ほか。estat-boundary-2020 は幾何が WKB の BLOB の素の列（ファイルに CRS の記録なし）。abr-src の代表点は文字列の緯度経度で、幾何ではない。geo-triples-* は幾何の列を持たない（設計上）。ne-admin0-10m は確認した 1 本に `geo` が見つからなかった（幾何の有無は未確認）。統計・テキスト系は幾何を持たない。
- **同じデータセットでも版で変わる**: jp-admin-2026-09 は、2026-09-28 に読んだカードでは「GeoParquet の geo メタデータは無い」とされていたが、2026-10-06 更新の HEAD（e6c87b1）では GeoParquet 1.1 で、municipalities は 47 の行グループ（最大 195 行）、`bbox` の列つき。カードより新しい。**カードの記述とファイルの現状は、日付と sha で突き合わせる**。

## 道具ごとの読まれ方（実測）

| 入口 | 対象 | 結果 | 出典 |
|---|---|---|---|
| DuckDB | Parquet（URL） | HEAD 1 回、GET を列ごと・行グループごとに数回（206）。形の列が大きく bbox 列が無いと、範囲で絞っても全体に近い | Yuiseki さん（2026-09-29 測定） |
| terrio 0.4.2 CLI | estat-boundary-2020 r2ka37.parquet（4.5 MB）の URL | 64 KiB の Range（206）のあと、全体を GET（302→CDN 200）、4,520,782 バイト受信 | 2026-10-24 実測 |
| terrio 0.4.2 CLI | 同 Parquet（ローカル） | 幾何を認識せず（`Geometry: None`、列は Blob） | 2026-10-24 実測 |
| terrio 0.4.2 CLI | jp-admin municipalities（ローカル 148.6 MB） | `MultiPolygon`、1,918、EPSG:4612。`--where "pref_code = '37'"` で 17 地物の GeoJSON が出て、属性の日本語も正しい | 2026-10-24 実測 |
| terrio CLI（0.3.2） | 他の Hugging Face の GeoParquet | 全量ダウンロード。中断すると一時ファイルが残る | kcai-terrio |
| terrio-js（WebAssembly） | GeoParquet の bbox 読み | 行グループが複数あり統計があれば範囲で飛ばせる（日本の建物 5 GB で 16 MiB）。Hugging Face の行グループ 1 つのものはほぼ全体（430 MB で約 394 MiB） | kcai-terrio |

- 実験（2026-10-24、estat-boundary-2020 の東京を手元で書き直した）: `geo` メタデータだけでは terrio-js も全量読みで、`bbox` 列と空間順の行グループまで足すと 6.9MB のうち 1.3MB で済んだ。terrio CLI は、どの変種でも全量だった。Hilbert 順で行グループを 100〜250 行にすると、東京の渋谷周辺は 9〜11% まで下がった。詳細は `checks/check-2026-10-24-estat-boundary-geoparquet.md`。
- 含意: 行グループの数と bbox covering の有無が、範囲読みの効き目を決める。estat-boundary-2020（行グループ 1）より、jp-admin HEAD（47 行グループ、covering あり）のほうが、範囲読みに向く作りになっている。
- jp-admin の 148.6 MB のファイルをリモートから `--where` 付きで読んだときの転送量は未確認（ローカルのファイルでだけ確認した）。

## 使い分けの目安（この踏み跡の仮説）

1. 必要な県・年・レイヤーが決まっているなら、型 B/C のファイル単位で取る（最大でも数十 MB のものが多い）。
2. 1 本が数百 MB 以上の型 A は、先にダウンロードしてローカルで読む。
3. 地物を扱う道具（terrio、GeoPandas、QGIS など）に渡す前に、`geo` メタデータの有無を見る。無いなら、前処理が要る。
4. 引用は `resolve/<コミット>/<パス>` で版を固定し、取得日を残す。

## 確かめなかったこと

- Hugging Face の datasets-server（`/parquet`、`/rows` など）や `hf://` のグロブ経由の挙動。
- 認証やレート制限。
- 全 69 件で全ファイルを見たわけではない（最大の Parquet 1 本のみ）。

## 出典

- Hugging Face API（2026-10-24）、Parquet のフッター取得
- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/README.md（コミット 6880b32）
- dwg7/kcai-terrio knowledge/cloud-native-read-behavior-matrix.md
- checks/check-2026-10-24-terrio-reads.md
