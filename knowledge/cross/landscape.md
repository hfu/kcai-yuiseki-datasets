---
id: yuiseki-datasets-landscape
title: Yuiseki さんの公開データセット群の見取り図
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/README.md（コミット 6880b32）
  - yuiseki/study-geoai-algo-py docs/datasets/README.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-index
  - yuiseki-datasets-categories
  - yuiseki-datasets-japan-admin-lineage
datasets:
  - yuiseki/estat-boundary-2020
  - yuiseki/jp-admin-2026-09
  - yuiseki/abr-src-2026-09
verified_how: read-docs
pattern: landscape
finding:
  - Hugging Face の yuiseki のデータセットは、一覧表の時点で「地理に関わるもの」が 45 件。出どころの違いと、日本の行政区画の連鎖（国勢調査境界→行政区画←住所基盤）が全体の骨格になっている
---

## 要点

- 2026-10-24 時点の全 69 件の索引と分類は `yuiseki-datasets-index`。この文書は、コミット 6880b32 の docs が書いていた時点（45 行）の見取り図。
- 一覧は `huggingface-yuiseki/README.md`。2026-09-28 の API 取得で 26 件と書かれているが、表はその後の更新（〜2026-10-10）を含み 45 行ある（コミット 6880b32 で数えた）。件数は版で変わるので、引くときは日付を添える。
- `docs/datasets/README.md` の本文は「Hugging Face の地理に関わる 20 個」と書く。これも別の時点の数で、README 同士で食い違う。どれが正しいかは未確認。
- 上位の `docs/datasets/README.md` は、Hugging Face 以外も含む出どころの目録（STAC カタログ、z.yuiseki.net、source.coop、uedayou.net、その他）。Hugging Face のデータセットはその一つの節。

## 表から見える系統（この踏み跡での整理。Yuiseki さんの分類ではない）

| 系統 | 例（一覧表の名前） |
|---|---|
| 日本の行政区画・境界 | estat-boundary-2020、jp-admin-2026-09、abr-src-2026-09、geo-triples-jp-gov |
| OSM とその周辺 | osm-tokyo23-src-2026-08、osm-japan-src-2026-08、osm-tokyo23-qa-2026-08、osm-wiki、osm-tag-corpus、text2geoql、geo-triples-japan、geo-triples-tokyo23 |
| 世界の統計・社会 | worldbank-wdi、pwt、maddison-project、undp-hdr、unhcr-refugee-stats、un-statistical-yearbook、undata-sdmx、ucdp-ged |
| 日本の公的な地物・災害・交通 | gsi-evacuation-sites-jp、gsi-global-map-jp、mlit-toshi-keikaku-jp、nfgis-2024、npa-traffic-accidents、mlit-1km-fromto-2022-01、ekidata-jp、env-redlist-jp |
| 世界の地名・地図・格子 | geonames、natural-earth、ne-admin0-10m、opencellid、ourairports-2026-08、worldpop-jp-2026-01、meta-move-dist、meta-range-maps-2022-05 |
| 文書・知識 | wikipedia-geotagged、wikivoyage-geotagged、wikidata-gazetteer、un-docs、gsj-reports、nilim-disaster-reports、osm-wikidata-brand-* |

- 一覧表は「地理に関わるもの」のほかに、地理と関係ない 6 件（onomatopoeia など）を「調べていない」として挙げている。

## 作りの特徴（一覧表と先頭の説明から）

- 1 データセット 1 ファイル。ライセンスと件数の区分は Hugging Face のタグの値。
- 凍結版（日付や commit を名前に持つ）と、上書き型（最新に追随）が混在する。例: gsi-evacuation-sites-jp は毎朝作り直される上書き型、osm-*-src-2026-08 は凍結。
- 版を積む形（geonames の夜ごと、opencellid の日付ごと）のものがある。
- ライセンスは cc-by-4.0 が多いが、odbl（OSM 系）、cc-by-sa-4.0（Wikipedia 系、opencellid）、cc0（wikidata-gazetteer）、other など。再配布の条件は一つずつ見る必要がある。

## つまずきやすい点

- 同じ「行政区画」でも、データセットごとに時点が違う（jp-admin は名前とコードが 2026-09、人口とポリゴンは 2020 年）。
- 件数や「いくつあるか」は、README の節ごとに時点が違い、そのまま比べられない。

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/README.md（コミット 6880b32）
- yuiseki/study-geoai-algo-py docs/datasets/README.md（コミット 6880b32）
