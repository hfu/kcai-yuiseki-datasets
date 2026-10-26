---
id: yuiseki-datasets-scale
title: yuiseki のデータセットの規模：全体の大きさ、Parquet の分け方、読み始める前に知りたい量
status: draft
sources:
  - Hugging Face API `/api/datasets?author=yuiseki` と `/api/datasets/<名前>?blobs=true`（2026-10-24 に取得。ファイル数とサイズ）
  - Parquet のフッター（末尾 1 MiB）の Range 取得（`geo` メタデータの有無。データセットごとに最大の Parquet 1 本のみ）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/README.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-index
  - yuiseki-datasets-growth-2026-10-26
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-landscape
  - yuiseki-datasets-terrio-usage-possibilities
verified_how: read-data
pattern: landscape
finding:
  - 2026-10-24 時点で yuiseki のデータセットは 69 件・合計約 58 GB。うち Parquet は約 21 GB で、残りは元の zip、gz、pbf、tif など。ほとんどは「1 県分ずつ」「1 表ずつ」に割れていて、必要な単位だけ取れる
---

## 要点

- 全 69 件の索引は `yuiseki-datasets-index`、個別の踏み跡は `knowledge/datasets/<名前>.md`。
- 一覧（コミット 6880b32 の `huggingface-yuiseki/README.md`）は 45 行だったが、API では 69 件（地理に関係ない古い 6 件を含む）。その後に、国土数値情報のバス（ksj-*）、国勢調査メッシュ（estat-census-mesh-*）、estat-jumin-idou、un-wpp、egov-laws-jp などが増えている。**件数と規模は日付つきで引く**。
- 全体は約 58.0 GB。Parquet は約 21.1 GB、残り（約 36.8 GB）は元の配布物（zip、gz、pbf、tif、csv、xlsx、dta、geojson、jsonl）。「元の配布物も一緒に置く」のが基本の作りで、データセットの総量は Parquet だけの量より大きい。
- 規模の分布（全体の大きさ）: 10 MB 未満 20 件、10〜100 MB 13 件、100 MB〜1 GB 23 件、1 GB 以上 13 件。
- いちばん大きいのは un-wpp（11.70 GB）、osm-japan-src-2026-08（9.26 GB）、worldpop-jp-2026-01（8.42 GB、ほぼ全部が GeoTIFF 2,048 本）。

## 規模を読むときの注意（意味づけ）

- **「大きい」の意味が3通りある**: (1) 全体の大きさ（元の zip も含む）、(2) Parquet の合計、(3) 1 回に読むことになる 1 ファイルの大きさ。読み始めるときに効くのは主に (3)。例: estat-boundary-2020 は全体 694.7 MB だが、Parquet は 47 本（最大 18.1 MB、北海道）。1 県なら 2.7〜18 MB で読める。
- **1 ファイルが大きいもの**: jp-admin-2026-09 の municipalities（148.6 MB、1,918 行。行数が少ないのは形が重いから）、wikidata-gazetteer（508 MB の 1 本）、un-docs（409 MB の 1 本）、egov-laws-jp（555 MB の 1 本）、osm-japan-src の planet_osm_polygon（約 4.2 GB）。terrio の CLI はリモートの Parquet を全量取得するため（実測は access-methods 参照）、これらは手元に落とす前提になる。
- **行数が少なくても重い**: 形（ポリゴン）の列がファイルの大部分を占める。jp-admin は 1,918 行で 148.6 MB（1 行あたり約 77 KB）、abr-src の町字（727,429 行）は 9.3 MB。「行数 ≒ 重さ」ではない。
- **版が積まれて増えるもの**: geonames（夜ごと）、opencellid（日付ごと）、worldbank-wdi（zip 7 版）、un-wpp。取得日で量が変わる。
- Parquet の件数は、データセットによって 1 本（osm-wiki、un-docs など）から 472 本（estat-jumin-idou）まで幅がある。

## 規模表（全体の大きい順。2026-10-24 の API）

「地物形式」は、データセットごとに最大の Parquet 1 本のフッターを見た結果。`geoparquet`＝GeoParquet の `geo` メタデータあり、`plain`＝なし、`no-parquet`＝Parquet 無し。plain には、そもそも地物を持たない表（統計、テキスト）も含む。1 本だけの確認なので、同じデータセットの他のファイルが違う可能性は残る。

| データセット | 最終更新 | ライセンス(タグ) | 全体 | ファイル数 | Parquet 本数 | Parquet 合計 | 最大の Parquet | 地物形式 |
|---|---|---|---|---|---|---|---|---|
| un-wpp | 2026-10-10 | other | 11.70 GB | 127 | 54 | 3.19 GB | 220.8 MB | plain |
| osm-japan-src-2026-08 | 2026-10-06 | odbl | 9.26 GB | 12 | 4 | 6.46 GB | 4.19 GB | geoparquet |
| worldpop-jp-2026-01 | 2026-10-02 | cc-by-4.0 | 8.42 GB | 2053 | 1 | 0.1 MB | 0.1 MB | plain |
| nfgis-2024 | 2026-10-10 | cc-by-4.0 | 2.68 GB | 105 | 48 | 1.26 GB | 214.9 MB | geoparquet |
| ilostat | 2026-10-10 | cc-by-4.0 | 2.66 GB | 2219 | 0 | - | - | no-parquet |
| mlit-toshi-keikaku-jp | 2026-10-06 | cc-by-4.0 | 2.65 GB | 177 | 26 | 626.4 MB | 134.5 MB | geoparquet |
| wikipedia-geotagged | 2026-09-24 | cc-by-sa-4.0 | 2.20 GB | 11 | 7 | 2.20 GB | 411.1 MB | plain |
| estat-jumin-idou | 2026-10-10 | other | 2.20 GB | 1891 | 472 | 458.2 MB | 21.7 MB | plain |
| faostat | 2026-10-10 | cc-by-4.0 | 1.52 GB | 72 | 0 | - | - | no-parquet |
| geonames | 2026-10-02 | cc-by-4.0 | 1.38 GB | 24 | 7 | 752.7 MB | 177.2 MB | geoparquet |
| natural-earth | 2026-10-06 | other | 1.28 GB | 427 | 215 | 450.3 MB | 50.7 MB | geoparquet |
| estat-census-mesh-250m-2020 | 2026-10-13 | cc-by-4.0 | 1.21 GB | 582 | 12 | 685.7 MB | 87.4 MB | plain |
| meta-move-dist | 2026-10-02 | cc-by-4.0 | 1.03 GB | 19 | 1 | 89.1 MB | 89.1 MB | plain |
| worldbank-wdi | 2026-10-03 | cc-by-4.0 | 875.0 MB | 67 | 42 | 370.1 MB | 50.4 MB | plain |
| wikidata-gazetteer | 2026-09-21 | cc0-1.0 | 863.4 MB | 6 | 2 | 863.4 MB | 508.4 MB | plain |
| estat-boundary-2020 | 2026-09-26 | cc-by-4.0 | 694.7 MB | 100 | 47 | 372.0 MB | 18.1 MB | plain |
| estat-census-mesh-500m-2020 | 2026-10-13 | cc-by-4.0 | 586.8 MB | 582 | 12 | 334.6 MB | 43.3 MB | plain |
| npa-traffic-accidents | 2026-10-01 | cc-by-4.0 | 579.1 MB | 76 | 21 | 110.4 MB | 18.1 MB | geoparquet |
| egov-laws-jp | 2026-10-07 | cc-by-4.0 | 554.7 MB | 5 | 1 | 554.7 MB | 554.7 MB | plain |
| undata-sdmx | 2026-10-06 | other | 514.9 MB | 691 | 8 | 16.0 MB | 5.9 MB | plain |
| ksj-n07-bus-route-jp | 2026-10-22 | cc-by-4.0 | 434.3 MB | 102 | 48 | 150.1 MB | 74.9 MB | geoparquet |
| un-docs | 2026-09-21 | other | 409.4 MB | 5 | 1 | 409.4 MB | 409.4 MB | plain |
| ucdp-ged | 2026-10-02 | cc-by-4.0 | 399.2 MB | 36 | 8 | 193.4 MB | 35.6 MB | geoparquet |
| gsj-reports | 2026-10-06 | cc-by-4.0 | 386.1 MB | 7 | 0 | - | - | no-parquet |
| ksj-l01-land-price | 2026-10-16 | cc-by-4.0 | 385.6 MB | 407 | 8 | 48.3 MB | 6.4 MB | plain |
| mlit-1km-fromto-2022-01 | 2026-10-01 | cc-by-4.0 | 317.3 MB | 109 | 5 | 116.6 MB | 104.1 MB | plain |
| osm-tokyo23-src-2026-08 | 2026-10-06 | odbl | 295.3 MB | 12 | 4 | 207.7 MB | 151.1 MB | geoparquet |
| pwt | 2026-10-05 | cc-by-4.0 | 265.7 MB | 157 | 41 | 41.4 MB | 2.1 MB | plain |
| estat-census-mesh-2020 | 2026-10-13 | cc-by-4.0 | 262.1 MB | 582 | 12 | 145.3 MB | 19.0 MB | plain |
| opencellid | 2026-10-06 | cc-by-sa-4.0 | 246.0 MB | 7 | 1 | 126.5 MB | 126.5 MB | geoparquet |
| jp-admin-2026-09 | 2026-10-06 | cc-by-4.0 | 228.6 MB | 6 | 2 | 228.6 MB | 148.6 MB | geoparquet |
| meta-range-maps-2022-05 | 2026-10-02 | cc-by-4.0 | 218.7 MB | 11 | 3 | 89.1 MB | 38.7 MB | plain |
| edgar-ghg-countries | 2026-10-10 | cc-by-4.0 | 190.8 MB | 14 | 0 | - | - | no-parquet |
| gsi-evacuation-sites-jp | 2026-10-06 | cc-by-4.0 | 177.4 MB | 15 | 2 | 9.8 MB | 5.7 MB | geoparquet |
| osm-wiki | 2026-09-17 | (なし) | 159.3 MB | 5 | 1 | 159.2 MB | 159.2 MB | plain |
| wikivoyage-geotagged | 2026-09-24 | cc-by-sa-4.0 | 101.7 MB | 5 | 1 | 101.6 MB | 101.6 MB | plain |
| ksj-p11-bus-stop-jp | 2026-10-23 | cc-by-4.0 | 98.0 MB | 102 | 48 | 15.3 MB | 7.3 MB | geoparquet |
| geo-triples-japan | 2026-09-26 | odbl | 86.2 MB | 9 | 3 | 86.2 MB | 62.5 MB | plain |
| gsi-global-map-jp | 2026-10-05 | cc-by-4.0 | 75.3 MB | 72 | 45 | 24.7 MB | 3.1 MB | geoparquet |
| moni1000-reports | 2026-10-07 | other | 57.6 MB | 4 | 0 | - | - | no-parquet |
| abr-src-2026-09 | 2026-09-26 | cc-by-4.0 | 50.1 MB | 66 | 7 | 22.4 MB | 9.3 MB | plain |
| open2ch-livejupiter-qa | 2024-04-01 | (なし) | 47.3 MB | 3 | 1 | 47.3 MB | 47.3 MB | plain |
| ne-admin0-10m | 2026-09-26 | other | 46.7 MB | 16 | 3 | 25.0 MB | 16.8 MB | plain |
| mlit-river-basin-overviews | 2026-10-07 | other | 37.8 MB | 4 | 0 | - | - | no-parquet |
| ourairports-2026-08 | 2026-10-02 | other | 33.3 MB | 19 | 7 | 8.6 MB | 5.0 MB | geoparquet |
| ksj-n07-bus-route-greater-tokyo | 2026-10-22 | cc-by-4.0 | 32.1 MB | 15 | 5 | 16.3 MB | 8.2 MB | geoparquet |
| maddison-project | 2026-10-05 | cc-by-4.0 | 27.2 MB | 25 | 6 | 0.6 MB | 0.2 MB | plain |
| un-statistical-yearbook | 2026-10-06 | other | 22.9 MB | 50 | 24 | 0.4 MB | 0.0 MB | plain |
| ekidata-jp | 2026-10-05 | other | 14.4 MB | 51 | 23 | 4.1 MB | 0.6 MB | geoparquet |
| ksj-p11-bus-stop-greater-tokyo | 2026-10-22 | cc-by-4.0 | 9.4 MB | 15 | 5 | 2.5 MB | 1.3 MB | geoparquet |
| geo-triples-tokyo23 | 2026-09-25 | odbl | 8.0 MB | 9 | 3 | 8.0 MB | 5.4 MB | plain |
| unhcr-refugee-stats | 2026-10-05 | cc-by-4.0 | 7.2 MB | 18 | 7 | 2.6 MB | 1.0 MB | plain |
| osm-tag-corpus | 2026-09-07 | odbl | 6.6 MB | 5 | 1 | 6.6 MB | 6.6 MB | plain |
| scp-jp-plain | 2024-03-24 | cc-by-sa-3.0 | 5.3 MB | 3 | 1 | 5.3 MB | 5.3 MB | plain |
| undp-hdr | 2026-10-05 | other | 5.3 MB | 17 | 2 | 2.6 MB | 1.5 MB | plain |
| nilim-disaster-reports | 2026-10-06 | cc-by-4.0 | 4.5 MB | 9 | 0 | - | - | no-parquet |
| mlit-underpass | 2026-10-17 | cc-by-4.0 | 2.8 MB | 64 | 48 | 0.7 MB | 0.2 MB | geoparquet |
| geo-triples-jp-gov | 2026-09-26 | cc-by-4.0 | 2.3 MB | 9 | 3 | 2.3 MB | 1.5 MB | plain |
| osm-wikidata-brand-jp | 2026-09-17 | odbl | 2.2 MB | 5 | 1 | 2.2 MB | 2.2 MB | plain |
| env-redlist-jp | 2026-10-05 | cc-by-4.0 | 0.8 MB | 21 | 8 | 0.3 MB | 0.1 MB | plain |
| osm-wikidata-brand-tokyo23 | 2026-09-17 | odbl | 0.6 MB | 5 | 1 | 0.6 MB | 0.6 MB | plain |
| osm-tokyo23-qa-2026-08 | 2026-09-23 | odbl | 0.4 MB | 5 | 1 | 0.4 MB | 0.4 MB | plain |
| onomatopoeia-ja | 2024-03-18 | mit | 0.3 MB | 3 | 1 | 0.3 MB | 0.3 MB | plain |
| g-uc | 2024-03-27 | (なし) | 0.3 MB | 3 | 1 | 0.3 MB | 0.3 MB | plain |
| onomatopoeia-ja-flat | 2024-03-19 | (なし) | 0.2 MB | 3 | 1 | 0.2 MB | 0.2 MB | plain |
| text2geoql | 2026-08-29 | odbl | 0.2 MB | 3 | 1 | 0.2 MB | 0.2 MB | plain |
| sake_qa | 2024-03-23 | mit | 0.1 MB | 3 | 1 | 0.1 MB | 0.1 MB | plain |
| osm-tokyo23-questions | 2026-09-23 | odbl | 0.1 MB | 6 | 1 | 0.0 MB | 0.0 MB | plain |
| rinya-forest-inventory | 2026-10-07 | other | 0.0 MB | 4 | 0 | - | - | no-parquet |

## 追加分（2026-10-26、新規27件）

- 2026-10-26 時点で **96 件**、合計 61.81 GB（Parquet は約 22.38 GB）。新規27件は合計 3.78 GB。上の表と数字は 2026-10-24 の 69 件のもの。
- 新規27件で最も大きいのは ksj-a31a-flood-tokyo23（1.47 GB、元 zip が約1.26GB）、microsoft-building-footprints（840.2 MB）、jma-rain-tokyo（282.3 MB）。1 ファイルが最も大きい Parquet は microsoft-building-footprints-kanto-2026-08-13（273.2 MB）、ksj-a31a-flood-tokyo23（106.6 MB）、worldpop-idn-population-2015-2030-1km-r2025a（94.3 MB）。
- 新規の Parquet の行数は、1件が数百行（nagaoka 166、kamisunagawa 105）から、agera5 の 47,507,200 行（年ごと48ファイル）まで幅が大きい。
- 「全国1本と県別」「全体1本とカテゴリ別」で行を二重に持つもの（ksj-a31a-flood-tokyo23）では、Parquet の行数の合計は実際の件数の2倍になる。

| データセット | 最終更新 | ライセンス(タグ) | 全体 | ファイル数 | Parquet 本数 | Parquet 合計 | 最大の Parquet | 地物形式 |
|---|---|---|---|---|---|---|---|---|
| ksj-a31a-flood-tokyo23 | 2026-10-26 | cc-by-4.0 | 1.47 GB | 17 | 6 | 213.4 MB | 106.6 MB | geoparquet |
| microsoft-building-footprints-kanto-2026-08-13 | 2026-10-25 | other | 840.2 MB | 11 | 2 | 390.5 MB | 273.2 MB | geoparquet |
| timezone-boundary-builder-2026d | 2026-10-25 | odbl | 333.9 MB | 18 | 3 | 211.7 MB | 90.0 MB | geoparquet |
| jma-rain-tokyo | 2026-10-26 | cc-by-4.0 | 282.3 MB | 1035 | 5 | 30.5 MB | 28.8 MB | plain |
| ghsl-japan-core-2020-30arcsec | 2026-10-25 | cc-by-4.0 | 177.7 MB | 34 | 10 | 154.0 MB | 16.5 MB | geoparquet |
| ibtracs-v04r01 | 2026-10-25 | other | 154.0 MB | 8 | 1 | 8.8 MB | 8.8 MB | geoparquet |
| gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2 | 2026-10-25 | cc0-1.0 | 127.1 MB | 10 | 1 | 36.9 MB | 36.9 MB | geoparquet |
| worldpop-idn-population-2015-2030-1km-r2025a | 2026-10-25 | other | 94.3 MB | 9 | 1 | 94.3 MB | 94.3 MB | geoparquet |
| agera5-japan-monthly-temperature-1979-2026 | 2026-10-25 | cc-by-4.0 | 84.6 MB | 56 | 48 | 83.8 MB | 1.8 MB | geoparquet |
| gsi-dem-fuji-z14-100m-2026-10-25 | 2026-10-25 | other | 52.5 MB | 105 | 1 | 1.7 MB | 1.7 MB | geoparquet |
| esa-worldcover-tokyo-2021-100m | 2026-10-25 | cc-by-4.0 | 34.1 MB | 17 | 1 | 4.8 MB | 4.8 MB | geoparquet |
| ctrees-agb-hokkaido-east-100m | 2026-10-25 | cc-by-4.0 | 27.9 MB | 19 | 1 | 2.1 MB | 2.1 MB | geoparquet |
| forty-hokkaido-east-2020 | 2026-10-25 | cc-by-4.0 | 20.5 MB | 15 | 1 | 12.8 MB | 12.8 MB | geoparquet |
| koppen-geiger-east-asia-1991-2020 | 2026-10-25 | cc-by-4.0 | 13.5 MB | 9 | 1 | 1.0 MB | 1.0 MB | geoparquet |
| gpw-grasslands-hokkaido-east-2018-2020-250m | 2026-10-25 | cc-by-4.0 | 13.3 MB | 9 | 1 | 4.8 MB | 4.8 MB | geoparquet |
| worldpop-kor-population-2015-2030-1km-r2025a | 2026-10-25 | other | 12.9 MB | 5 | 1 | 12.9 MB | 12.9 MB | geoparquet |
| kontur-population-2023-11-01-22km | 2026-10-25 | other | 10.2 MB | 7 | 1 | 3.5 MB | 3.5 MB | geoparquet |
| akita-kumadas-wildlife-sighting | 2026-10-26 | cc-by-4.0 | 8.5 MB | 9 | 1 | 2.1 MB | 2.1 MB | geoparquet |
| usgs-comcat-2025-m45 | 2026-10-25 | other | 6.7 MB | 8 | 1 | 0.6 MB | 0.6 MB | geoparquet |
| gebco-2026-hokkaido-east-15as | 2026-10-25 | other | 3.9 MB | 4 | 1 | 3.9 MB | 3.9 MB | geoparquet |
| tokyo-flood-record-jp | 2026-10-26 | cc-by-4.0 | 3.2 MB | 54 | 2 | 1.1 MB | 1.1 MB | geoparquet |
| kyoto-bear-sighting | 2026-10-26 | cc-by-4.0 | 2.7 MB | 9 | 1 | 0.6 MB | 0.6 MB | geoparquet |
| forest-typology-validation-2020 | 2026-10-25 | cc-by-4.0 | 1.6 MB | 9 | 2 | 0.7 MB | 0.3 MB | geoparquet |
| ishikawa-bear-incident | 2026-10-26 | cc-by-4.0 | 1.2 MB | 19 | 6 | 0.3 MB | 0.2 MB | geoparquet |
| gifu-bear-sighting | 2026-10-26 | cc-by-4.0 | 1.2 MB | 31 | 12 | 0.5 MB | 0.1 MB | geoparquet |
| nagaoka-bear-sighting | 2026-10-26 | cc-by-4.0 | 0.2 MB | 14 | 1 | 0.0 MB | 0.0 MB | geoparquet |
| kamisunagawa-higuma-sighting | 2026-10-26 | cc-by-4.0 | 0.1 MB | 13 | 1 | 0.0 MB | 0.0 MB | geoparquet |

## 確かめなかったこと

- 行数、列数、行グループ数は、手元に落とした数本（estat-boundary-2020 の 2 県、abr-src の 6 本、jp-admin の 2 本、geo-triples-jp-gov の triples）しか数えていない。全体の行数は各カードに依る。
- 「元の配布物」が Parquet と同じ内容かどうかは見ていない。
- API の `size` は LFS を含むファイルサイズで、圧縮後の値。展開後の量は別。

## 出典

- Hugging Face API（2026-10-24）、Parquet フッターの Range 取得
- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/README.md（コミット 6880b32）
