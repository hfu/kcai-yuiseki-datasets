---
id: yuiseki-datasets-code-systems
title: コード体系の違いと、結合で落ちる穴：JIS、警察、FIPS、M49、メッシュ、Wikidata
status: draft
sources:
  - yuiseki/npa-traffic-accidents、geonames、un-statistical-yearbook、undp-hdr、estat-census-mesh-2020、mlit-1km-fromto-2022-01、ne-admin0-10m、meta-range-maps-2022-05、ourairports-2026-08、abr-src-2026-09、estat-boundary-2020、jp-admin-2026-09 のカード（Hugging Face 上の main、2026-10-24 取得）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-patterns-regional-keys
  - yuiseki-datasets-japan-admin-lineage
  - yuiseki-datasets-version-policies
verified_how: read-docs
pattern: pattern
finding:
  - 「都道府県コード」「国コード」と呼ばれる列が、データセットによって別の体系で、同じ名前でも結合できない。結合の前に体系・桁・型・版を明示する
---

## 要点

- 同じ日本の都道府県でも、データセットによって使うコード体系が違う。名前が似ているだけで結合すると、行が静かにずれる。

## 体系の対比（カードの記述）

| データセット | 列 | 体系 | 注意 |
|---|---|---|---|
| jp-admin-2026-09、abr-src-2026-09 | `lg_code`（6桁）、`code5`（5桁）、`pref_code` | JIS（全国地方公共団体コード） | 先頭のゼロを守るため文字列 |
| estat-boundary-2020 | `KEY_CODE`、`PREF`+`CITY`+`S_AREA` | 国勢調査の小地域キー | KEY_CODE の桁が2・9・11桁と混在。11桁を自分で作る |
| npa-traffic-accidents | `都道府県コード` | 警察独自 | 東京は 13 でなく 30。北海道は方面本部ごとに5コード |
| geonames | `admin1_code` | 主に FIPS | 日本は 01 愛知〜47 沖縄のローマ字順。JIS（北海道が01）と違う |
| un-statistical-yearbook | `area_code` | 国連 M49 | 日本は 392。1 は全体、2 はアフリカなど集計も同じ列。0 は「合計」 |
| undp-hdr | `iso3` | ISO 3166-1 alpha-3 | `ZZ` で始まる11行は集計（HDI グループ、地域、世界） |
| estat-census-mesh-* | `KEY_CODE`（8桁） | 基準地域メッシュ | JGD2000 版と JGD2011 版があり、20県で内容が違う。混ぜない |
| mlit-1km-fromto-2022-01 | `prefcode`、`citycode`、`month` | JIS + 文字列 | 属性表とマスターに2019/2020版があり、`version` を揃えないと行が倍になる。2019年版の福岡県中川市は旧町のコード40305 |
| ne-admin0-10m | `WIKIDATAID`（国）、`wikidataid`（州） | Wikidata の Q | 列名の大文字小文字が層で違う |
| meta-range-maps-2022-05 | 地域名と `polygon_id` | Meta 独自 | 名前が `NA` の地域が898。`polygon_id` で結ぶ |
| ourairports-2026-08 | `regions.local_code` | OurAirports 独自 | 引用符なしのゼロつきコードで、型推論が数値にする |
| estat-jumin-idou | `statsDataId` と分類の slot | e-Stat 独自 | 表ごとに分類軸の意味が違い、`tables` で確認する |

- **追加（2026-10-30、実測で訂正）**: 東北6県の森林資源メッシュは平面直角座標系で、福島だけ EPSG:6677（第IX系）、他の5県は EPSG:6678（第X系）。同じ県の現存植生図は6県とも幾何が EPSG:6668（JGD2011の経緯度）で、面積列（`area_m2`）だけ EPSG:6678（第X系）で計算されている。メッシュと植生図を重ねるには、**6県とも再投影が要る**。メッシュのセルの座標（`cell_x`・`cell_y`）はメッシュの座標系のメートル。

## 使うときの注意（意味づけ）

- **体系の変換表が要る組**: 警察コードと JIS（npa-traffic-accidents × jp-admin）、FIPS と JIS（geonames × jp-admin）、M49 と ISO3（un-statistical-yearbook × undp-hdr）。変換表はデータセット側には無いので、別途用意する（未確認）。
- **桁と型**: ゼロつきコードを持つデータセットは、全列を文字列にして先頭のゼロを守っている（abr-src、estat-boundary、mlit-1km-fromto、npa-traffic-accidents、estat-census-mesh）。読む側で数値化すると結合が壊れる。
- **時点**: 市区町村のコードは廃置分合で変わる（例: 福岡県中川市の旧コード）。時点の違うコードを結ぶと欠ける（浜松市の新3区など）。

## 確かめなかったこと

- 表の内容はカードの記述を整理したもの。変換表の存在、各コードの網羅性は確認していない。
- 全データセットのコード列を網羅したわけではない（カードで体系に注意が書かれていたものを挙げた）。

## 出典

- 上記データセットのカード（個別の踏み跡の出典欄を参照）
- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
