---
id: yuiseki-datasets-card-vs-data-checks
title: カードの記述と実データの突き合わせ：一致したこと、食い違ったこと、元データ由来の欠陥
status: draft
sources:
  - yuiseki/ 配下の各データセットのカード（Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター・全行の文字検査（2026-10-24、duckdb）
  - Natural Earth 配布 zip（yuiseki/ne-admin0-10m 内の v5.1.1 の元 zip）の DBF
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-index
  - yuiseki-datasets-scale
  - yuiseki-datasets-text-corpora
  - yuiseki-datasets-version-policies
verified_how: read-data
pattern: re-walk
finding:
  - カードの件数は多くの場合実測と一致した。食い違いは、カード冒頭の取り違え、カードより新しいコミット、全国と県別の二重計上、元データ由来の文字化けの4種類に分かれた
---

## 要点

- 各データセットのカードには、作者自身の検証（「Checked before upload」。ハッシュ、行数、全値の突き合わせ）が書かれている。ここでは、それとは別に、Parquet のフッターと全行の文字検査で、カードの件数と文字の状態を確かめた。
- 確かめたのは件数と文字の状態に限る。カードの検証（元ファイルとの全値一致など）を、元ファイルまで戻って再現してはいない。

## 一致したもの

| データセット | カードの数 | 実測 |
|---|---|---|
| estat-boundary-2020 | 232,019 行 | 同じ（47本の合計。前回の確認） |
| jp-admin-2026-09 | 47 + 1,918 行 | 1,965（同じ） |
| geo-triples-jp-gov | 162,810 / 165,670 / 1,807 | 同じ |
| natural-earth | 357,763 地物 | 215本のフッターの合計で同じ |
| estat-census-mesh-2020 / 250m / 500m | 2,134,320 / 13,975,584 / 5,604,594 行 | 同じ |
| wikipedia-geotagged | 英 1,374,056 + 日 218,496 | 1,592,552（同じ） |
| wikivoyage-geotagged | 29,505 | 同じ |
| un-docs | 39,363 | 同じ |
| wikidata-gazetteer | 場所 12,205,328 + 名前 62,506,107 | 2本の合計 74,711,435（同じ） |
| ksj-n07/p11、mlit-underpass | 354,208 / 278,515 / 3,841 など | Parquet の合計は全国1本と県別の二重計上でちょうど2倍。半分がカードの数 |
| osm-wikidata-brand-jp / tokyo23 | 1,859 / 892 ブランド | 同じ |
| worldpop-jp-2026-01 | 1,024 ラスタ | 一覧の1,024行 |

## 食い違ったもの

| データセット | 食い違い | 種類 |
|---|---|---|
| geo-triples-japan | カード冒頭の件数（510,616 トリプルなど）は geo-triples-tokyo23 のもの。実データは 3,286,232 / 4,678,910 / 68,025 行で、本文の表の数字と一致 | カード冒頭の取り違え |
| geo-triples-tokyo23 | 冒頭は評価問題 8,890、本文は 8,854。実測 8,854 | カード内の不一致 |
| jp-admin-2026-09 | study-geoai-algo-py の docs（2026-09-28）は GeoParquet メタデータ無しとしたが、HEAD（e6c87b1、2026-10-06）は GeoParquet 1.1・47行グループ・bbox 列つき | カードより新しいコミット |
| estat-jumin-idou | 全472本の合計 214,274,872 行。カードの観測数は 214,274,401 で、471 の差は `tables`（471行）の分と合う | 数え方の違い |
| un-wpp | 現行 WPP2024 のカードは 53 表・200,840,623 行。実際の Parquet は 54 本・合計 200,840,676 行で、差は 53 行。差の内訳は未確認 | 未解決 |
| 前回の踏み跡（study-geoai-algo-py 読み取り） | `abr-src` のカードは町字 727,428 行、実測 727,429（廃止予定の1行の数え方）、「26 件」「45 行」「69 件」など、件数の時点の違い | 時点の違い |

## 追加分（2026-10-26、新規27件）の突き合わせ

- **件数が一致したもの**: akita（24,757）、gifu（6,946）、ishikawa（3,901）、kamisunagawa（105）、kyoto（10,225）、nagaoka（166）、tokyo-flood-record-jp（5,845+121=5,966）、jma-rain-tokyo（日別588,783+時別8,660,976 ほか）、gfw（34,516,630）、gebco（518,400）、esa-worldcover（360,000）、ghsl（7,200,000×2）、worldpop-kor（130,927）、agera5（47,507,200）、microsoft-building-footprints（5,781,554）、usgs（8,502）、koppen（13,480）、forty（63,630）、forest-typology-validation（9,100+8,190=17,290）。
- **数え方の違い**: ksj-a31a-flood-tokyo23 の Parquet 全行 455,302 は、全体1本とカテゴリ別5本の二重計上で、実際は 227,651（カードの件数）。
- **文字（実測）**: ishikawa-bear-incident の `forest_r1_r6` の `remarks`（2,423行）に U+FFFD が17行。それ以外の文字列の列を持つ新規は、検査した範囲で U+FFFD も二重エンコードの疑いも無かった。
- **欠損（実測）**: usgs-comcat の `tz` は全行null、`felt` 84%、`mmi` 90%。tokyo-flood-record-jp の `district3` 99.7%、`pd_bldg` 98%。ibtracs の `WMO_WIND` 61%、`WMO_PRES` 58%。いずれもカードの記述と矛盾しない（カードは欠損の割合を書かない）。
- 確かめた範囲（件数と、文字列の列の文字の状態）では、カードとデータの食い違いは見つかっていない。

## 追加分（2026-10-30、新規20件）の突き合わせ

- **件数が一致したもの**: 東北6県の森林資源メッシュ（秋田29,088,595、青森24,108,678、福島34,452,709、岩手38,179,256、宮城18,194,823、山形23,319,199）、植生図（秋田174,576、青森147,302、福島336,047、岩手248,187、宮城143,044、山形141,922）、fagus-crenata-masting（102+102+19+6,747=6,970）、igrf-14（5,265）、agera5-water（47,507,200）、ksj-a31a-greater-tokyo（4,366,127。Parquet 全行は二重計上で8,732,254）。
- **数え方の違い**: aomori-forest-resource-mesh のカードは63シートと書くが、Parquet は62本（行数の合計はカードのセル数と一致。1シートが省略されたとみられるが未確認）。
- **座標系の違い（データセットの間）**: 森林資源メッシュは投影座標（福島だけ EPSG:6677 第IX系、他の5県は EPSG:6678 第X系）、現存植生図は6県とも EPSG:6668（経緯度）で面積列だけ EPSG:6678。カードはそれぞれ正しく書いている。（最初の版で、植生図の幾何を EPSG:6678 と書いた誤りを、`geo` メタデータの実測で訂正した。）
- **文字（実測）**: 文字列の列を持つ新規20件のうち検査した範囲（メッシュ6件の1ファイル各約75万行、fagus、landsat5、igrf、ksj-a31a-greater、miyagi-vegetation）で、U+FFFD も二重エンコードの疑いも無かった。130MB を超える植生図5件は未検査。
- カードとデータの食い違いは、確かめた範囲（件数、座標系の記述）では上の1件（63シート対62本）のみ。

## 元データ由来の文字の欠陥（Parquet は忠実に保持）

- **Natural Earth の DBF の二重エンコード:** 元 zip の `ne_10m_admin_1_states_provinces.dbf`（`.cpg` は UTF-8）で、`woe_label` の `Paysandú` が UTF-8 のバイト `C3 83 C2 BA`（`PaysandÃº`）で入っている。4,596 行中、`Ã` を含むのは 134 行。yuiseki/ne-admin0-10m の Parquet も同じ文字列。カードは変換時に「`.cpg` が指す文字コードで復号した」と書いており、元の欠陥を直していない。natural-earth の別レイヤー（`ne_10m_admin_1_states_provinces_lakes`）の先頭 3,000 行にも同じ現象がある。
- **ucdp-ged:** `source_article`、`source_headline`（報道の引用）に、二重エンコードの疑いが少数（26.1 で 16 / 15 行、41.8万行中）。
- **g-uc:** 全 3,344 行のうち `place` 28 行、`person` 5 行に U+FFFD（出どころはカードが空）。
- その他、wikipedia-geotagged、wikivoyage-geotagged、geonames、open2ch-livejupiter-qa に、数行規模の疑い（個別の踏み跡を参照）。

## 使うときの注意（意味づけ）

- 件数を引くときは、カードの冒頭だけでなく、本文の表と Parquet のフッターを見る。
- Parquet の行数の合計は、全国ファイルと県別ファイルを両方持つデータセット（ksj-*、mlit-underpass）で二重になる。
- 文字の欠陥が元データ由来のときは、Parquet 側では直せない。使う側で修復するか、そのレイヤー・列を避ける。

## 確かめなかったこと

- 全行の文字検査は、データセットごとに最大で2ファイル（130MB 以下）まで。130MB を超えるファイルしか無いデータセット（egov-laws-jp、osm-japan-src、osm-wiki、un-docs、wikidata-gazetteer）は未検査。natural-earth は215本中2本のみ。
- 二重エンコードの検査は、`Â`・`Ã`・`â` の直後に U+0080〜U+00BF が続く形だけを見ている。他の種類の化けは見ていない。正規の文章が当たる可能性がある（疑いとして扱った）。
- un-wpp の 53 行の差の原因は未確認。

## 出典

- 各データセットのカード、Hugging Face API（2026-10-24）
- Parquet のフッターと全行の文字検査（2026-10-24）
- yuiseki/ne-admin0-10m の元 zip（v5.1.1）の DBF
