---
id: yuiseki-datasets-landscape
title: Yuiseki さんの公開データセット群の見取り図
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/README.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related: []
datasets:
  - yuiseki/estat-boundary-2020
  - jp-admin-2026-09
  - abr-src-2026-09
verified_how: read-card
pattern: landscape
finding:
  - Yuiseki さんの公開データセット群は、境界・行政区画・統計・地理空間・時系列の大きく 5 つに見え、どれも「出どころを指す」形で整理されている
---

## 要点

- 見取り図としては、Yuiseki さんの公開データセット群は大きく 5 つの系統に分けられる。
- 境界・行政区画系は、統計や空間関係の結合の基礎になる。
- 統計系は、国勢調査・国連・世界銀行・為替・人口に関する表データが中心で、時系列の比較に向く。
- 空間関係・地理的文脈系は、隣接・包含や POI などの関係を表している。
- OSM や衛星・地図のような地理データは、二次利用のために型づけされた Parquet 形式が多い。

## 短く見渡す

- 境界・行政区画: `estat-boundary-2020`, `jp-admin-2026-09`, `abr-src-2026-09`, `geo-triples-jp-gov`
- 統計・人口・社会: `estat-census-basic`, `estat-jumin-idou`, `worldbank-wdi`, `pwt`, `undp-hdr`, `unhcr-refugee-stats`
- 地理的関係: `geo-triples-japan`, `geo-triples-tokyo23`, `nominatim-wikimedia-importance`
- 地図・地物・利用データ: `gsi-global-map-jp`, `gsi-evacuation-sites-jp`, `osm-...`, `natural-earth`, `opencellid`
- テキスト・文書・知識: `wikipedia-geotagged`, `wikidata-gazetteer`, `un-docs`, `osm-wiki`

## どんな切り方が有望か

- 地理空間の単位で切る: 県/市区町村/小地域/メッシュ/タイル/点
- 出どころで切る: e-Stat / GSI / OSM / World Bank / UN / Natural Earth
- 形で切る: 点・線・面・表・文
- 時点の扱いで切る: 凍結版 / 更新版 / 連続的な版ごとの上書き

## つまずきやすい点

- 同じ「市区町村コード」でも、時点によって定義や表記が異なることがある。
- 地方公共団体の境界と行政統計の境界が、必ずしも完全には一致しない。
- 一行一地域の表と、ポリゴンや点群の表は、同じ名前でも結合の粒度が違う。

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/README.md（コミット 6880b32）
