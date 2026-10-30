---
id: yuiseki-datasets-index
title: yuiseki のデータセット全116件の索引：分類、中身、規模、踏み跡
status: draft
sources:
  - Hugging Face API `/api/datasets?author=yuiseki`（2026-10-26）
  - 各データセットのカード（Hugging Face 上の main）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-landscape
  - yuiseki-datasets-growth-2026-10-26
  - yuiseki-datasets-scale
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-version-policies
  - yuiseki-datasets-rights-exclusions
  - yuiseki-datasets-code-systems
  - yuiseki-datasets-text-corpora
verified_how: read-docs
pattern: landscape
finding:
  - 2026-10-30 時点で116件。日本の公的データ、OSM とその派生、世界の統計、世界の地理、知識・テキスト、旧作に、2026-10-25〜30 に増えた9群（北海道東部の窓抽出、クマ出没記録、災害・気象、気候、人口・建物・土地被覆、地形・基盤、東北6県の森林資源・植生、ブナの豊凶、気象・地球物理の原本）を加えて分けると、全件に個別の踏み跡がある
---

## 要点

- 全 116 件（`knowledge/datasets/` に 1 件 1 ファイル。2026-10-30 時点）。分類はこの踏み跡での整理で、Yuiseki さんの分類ではない。増加の概観は `yuiseki-datasets-growth-2026-10-26`（2026-10-26 の27件と、2026-10-30 追記の20件）。
- 横断の踏み跡: 規模（`yuiseki-datasets-scale`）、アクセス方法（`yuiseki-datasets-access-methods`）、版の持ち方（`yuiseki-datasets-version-policies`）、権利の除外（`yuiseki-datasets-rights-exclusions`）、コード体系（`yuiseki-datasets-code-systems`）、テキスト系（`yuiseki-datasets-text-corpora`）。

## 一覧

### 日本の統計・公的GIS（22件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [abr-src-2026-09](../datasets/abr-src-2026-09.md) | アドレス・ベース・レジストリの町字72.7万件と代表点(境界なし) | 50.1 MB | cc-by-4.0 |
| [ekidata-jp](../datasets/ekidata-jp.md) | 鉄道事業者・路線・駅・隣接駅(join)・都道府県のマスター | 14.4 MB | other |
| [env-redlist-jp](../datasets/env-redlist-jp.md) | 環境省の第5次レッドリスト(分類群ごとの CSV 原本と Parquet 8本) | 0.8 MB | cc-by-4.0 |
| [estat-boundary-2020](../datasets/estat-boundary-2020.md) | 2020年国勢調査の小地域(町丁・字等)232,019件のポリゴンと人口・世帯数。県別 Parquet 47本 | 694.7 MB | cc-by-4.0 |
| [estat-census-mesh-2020](../datasets/estat-census-mesh-2020.md) | 2020年国勢調査を3次メッシュ(1km)ごとに集計した12表×47都道府県(564ファイル、213万行) | 262.1 MB | cc-by-4.0 |
| [estat-census-mesh-250m-2020](../datasets/estat-census-mesh-250m-2020.md) | 2020年国勢調査を250m(4分の1地域メッシュ)ごとに集計した12表×47都道府県(564ファイル、1,397万行) | 1.21 GB | cc-by-4.0 |
| [estat-census-mesh-500m-2020](../datasets/estat-census-mesh-500m-2020.md) | 2020年国勢調査を500m(2分の1地域メッシュ)ごとに集計した12表×47都道府県(564ファイル、560万行) | 586.8 MB | cc-by-4.0 |
| [estat-jumin-idou](../datasets/estat-jumin-idou.md) | 住民基本台帳人口移動報告の全471表・2.14億値を縦持ちにしたもの | 2.20 GB | other |
| [geo-triples-jp-gov](../datasets/geo-triples-jp-gov.md) | 行政区画ポリゴン同士の空間関係(GeoSPARQL の Simple Features 8述語、DE-9IM、RCC8)を1行1三つ組にした表と、文にした表、評価問題 | 2.3 MB | cc-by-4.0 |
| [gsi-evacuation-sites-jp](../datasets/gsi-evacuation-sites-jp.md) | 指定緊急避難場所と指定避難所の全国データ(CSV と GeoJSON と GeoParquet) | 177.4 MB | cc-by-4.0 |
| [gsi-global-map-jp](../datasets/gsi-global-map-jp.md) | 行政界・水系・人口集中地区・交通のベクタ(版×レイヤー別45本の GeoParquet)と、標高・土地被覆などのラスタ4種(元 zip のみ) | 75.3 MB | cc-by-4.0 |
| [jp-admin-2026-09](../datasets/jp-admin-2026-09.md) | 47都道府県と1,918市区町村のコード・名前・ポリゴン・人口(GeoParquet 1.1) | 228.6 MB | cc-by-4.0 |
| [ksj-l01-land-price](../datasets/ksj-l01-land-price.md) | 地価公示の標準地(1点=1区画)の価格・住所・面積・用途・都市計画などの約100属性 | 385.6 MB | cc-by-4.0 |
| [ksj-n07-bus-route-greater-tokyo](../datasets/ksj-n07-bus-route-greater-tokyo.md) | 埼玉・千葉・東京・神奈川(都道府県コード11〜14)のバス路線58,823本 | 32.1 MB | cc-by-4.0 |
| [ksj-n07-bus-route-jp](../datasets/ksj-n07-bus-route-jp.md) | 全国のバス路線354,208本(事業者名つき線) | 434.3 MB | cc-by-4.0 |
| [ksj-p11-bus-stop-greater-tokyo](../datasets/ksj-p11-bus-stop-greater-tokyo.md) | 埼玉・千葉・東京・神奈川のバス停44,101件 | 9.4 MB | cc-by-4.0 |
| [ksj-p11-bus-stop-jp](../datasets/ksj-p11-bus-stop-jp.md) | 全国のバス停278,515件(名称・事業者・停車する系統とその種別) | 98.0 MB | cc-by-4.0 |
| [mlit-1km-fromto-2022-01](../datasets/mlit-1km-fromto-2022-01.md) | 1kmメッシュごとの月別平均滞在人口と、居住地別の市区町村間流動(平日/休日、昼/深夜) | 317.3 MB | cc-by-4.0 |
| [mlit-toshi-keikaku-jp](../datasets/mlit-toshi-keikaku-jp.md) | 約1,400市区町村の都市計画決定(用途地域・都市計画道路・公園・地区計画・立地適正化計画など) | 2.65 GB | cc-by-4.0 |
| [mlit-underpass](../datasets/mlit-underpass.md) | 前後より著しく低い道路区間(アンダーパス)3,841点 | 2.8 MB | cc-by-4.0 |
| [nfgis-2024](../datasets/nfgis-2024.md) | 国有林の小班975,666、林班58,293、林道57,912(合計1,091,871地物) | 2.68 GB | cc-by-4.0 |
| [npa-traffic-accidents](../datasets/npa-traffic-accidents.md) | 人身事故1件=1行(本票)と補充票・高速票 | 579.1 MB | cc-by-4.0 |

### OSM とその派生（11件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [geo-triples-japan](../datasets/geo-triples-japan.md) | OSM の日本の行政区画とPOIの空間関係の三つ組(triples 3,286,232行)、文(cpt 4,678,910行)、評価問題(probe 68,025行) | 86.2 MB | odbl |
| [geo-triples-tokyo23](../datasets/geo-triples-tokyo23.md) | 東京23区とPOIの空間関係の三つ組(triples 510,616行)、文(cpt 483,922行)、評価問題(probe 8,854行) | 8.0 MB | odbl |
| [osm-japan-src-2026-08](../datasets/osm-japan-src-2026-08.md) | 全国のOSM凍結 pbf(2.8GB)と osm2pgsql 形式の Parquet 4表(点・線・面ほか) | 9.26 GB | odbl |
| [osm-tag-corpus](../datasets/osm-tag-corpus.md) | OSM のタグ9,803種の多言語説明・関連語・世界での使用回数 | 6.6 MB | odbl |
| [osm-tokyo23-qa-2026-08](../datasets/osm-tokyo23-qa-2026-08.md) | 215問の答えと、それぞれを導いた SQL/Overpass QL | 0.4 MB | odbl |
| [osm-tokyo23-questions](../datasets/osm-tokyo23-questions.md) | OSM から答えられるよう書かれた23区の英語の質問215問 | 0.1 MB | odbl |
| [osm-tokyo23-src-2026-08](../datasets/osm-tokyo23-src-2026-08.md) | 23区のOSM凍結 pbf と osm2pgsql 形式の Parquet 4表(点30.7万、面143.7万) | 295.3 MB | odbl |
| [osm-wiki](../datasets/osm-wiki.md) | OSM Wiki 8言語78,178ページの平文 | 159.3 MB | （なし） |
| [osm-wikidata-brand-jp](../datasets/osm-wikidata-brand-jp.md) | 全国の店舗チェーン1,859ブランド・172,852地物の、OSM 表記と Wikidata 名の対照 | 2.2 MB | odbl |
| [osm-wikidata-brand-tokyo23](../datasets/osm-wikidata-brand-tokyo23.md) | 23区の店舗チェーン892ブランド・25,407地物の、OSM 表記と Wikidata 名の対照 | 0.6 MB | odbl |
| [text2geoql](../datasets/text2geoql.md) | 小型言語モデル向けの合成データ | 0.2 MB | odbl |

### 世界の統計（12件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [edgar-ghg-countries](../datasets/edgar-ghg-countries.md) | 国別・IPCCセクター別の年次・月次排出量(1970〜2025年、F-gases は1990〜)を、JRC の xlsx の zip のまま8本保持 | 190.8 MB | cc-by-4.0 |
| [faostat](../datasets/faostat.md) | 66のドメイン zip(Normalized の長持ち CSV と、地域・品目・要素・フラグの辞書) | 1.52 GB | cc-by-4.0 |
| [ilostat](../datasets/ilostat.md) | 1,963指標ファイル(.csv.gz)、約3.99億レコード、目次(英仏西)と辞書244ファイル | 2.66 GB | cc-by-4.0 |
| [maddison-project](../datasets/maddison-project.md) | 西暦1年から現在までの一人当たり実質GDPと人口 | 27.2 MB | cc-by-4.0 |
| [pwt](../datasets/pwt.md) | PWT の7リリース | 265.7 MB | cc-by-4.0 |
| [ucdp-ged](../datasets/ucdp-ged.md) | 1989年以降の組織的暴力のイベント1件=1行(場所・日時・当事者・死者数) | 399.2 MB | cc-by-4.0 |
| [un-statistical-yearbook](../datasets/un-statistical-yearbook.md) | 国連統計年鑑の表(SYB68 の32表、SYB61 の1表) | 22.9 MB | other |
| [un-wpp](../datasets/un-wpp.md) | 1950年からの推計と2100年までの推計(年齢・性別、出生、死亡、生命表、純移動) | 11.70 GB | other |
| [undata-sdmx](../datasets/undata-sdmx.md) | エネルギー統計・エネルギーバランス・国民経済計算の主要集計・SEEA(大気排出とエネルギー)の5データフロー、539万観測 | 514.9 MB | other |
| [undp-hdr](../datasets/undp-hdr.md) | 人間開発指数(HDI)とGDI・IHDI・GII・PHDI、構成要素、統計付録表、多次元貧困指数(MPI) | 5.3 MB | other |
| [unhcr-refugee-stats](../datasets/unhcr-refugee-stats.md) | 難民・庇護申請者・国内避難民・無国籍者などの、出身国×庇護国×年の人数、庇護の申請と決定、帰還・再定住・帰化、年齢性別内訳 | 7.2 MB | cc-by-4.0 |
| [worldbank-wdi](../datasets/worldbank-wdi.md) | WDI の全指標×国×年を縦持ちにしたもの | 875.0 MB | cc-by-4.0 |

### 世界の地理（8件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [geonames](../datasets/geonames.md) | 1,350万地名・1,900万別名・行政階層・小さな表 | 1.38 GB | cc-by-4.0 |
| [meta-move-dist](../datasets/meta-move-dist.md) | 217か国の行政区×日ごとに、ふだんの居場所から離れた距離の割合(0km・10km未満・10〜100km・100km超) | 1.03 GB | cc-by-4.0 |
| [meta-range-maps-2022-05](../datasets/meta-range-maps-2022-05.md) | COVID-19 期の移動量の変化(2020年2月比)と1つの小域に留まった割合 | 218.7 MB | cc-by-4.0 |
| [natural-earth](../datasets/natural-earth.md) | 国・州・境界線・居住地・道路・鉄道・空港・港・時間帯・海岸線・河川など215レイヤーを、レイヤーごとの GeoParquet と元 zip で提供 | 1.28 GB | other |
| [ne-admin0-10m](../datasets/ne-admin0-10m.md) | 国258、州・省4,596、米国の郡3,224の3層を、zip と型付き Parquet で凍結 | 46.7 MB | other |
| [opencellid](../datasets/opencellid.md) | 携帯基地局のセル1つ=1行(識別子と推定位置) | 246.0 MB | cc-by-sa-4.0 |
| [ourairports-2026-08](../datasets/ourairports-2026-08.md) | 空港・ヘリポート・飛行場86,002件と滑走路・周波数・航法援助 | 33.3 MB | other |
| [worldpop-jp-2026-01](../datasets/worldpop-jp-2026-01.md) | 100m・1km のセルごとの人口、1kmの性別5歳階級、都市化度 | 8.42 GB | cc-by-4.0 |

### 知識・テキスト（10件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [egov-laws-jp](../datasets/egov-laws-jp.md) | 現行・施行予定の法令の改正版ごとに1行(原本XMLとテキスト抽出) | 554.7 MB | cc-by-4.0 |
| [gsj-reports](../datasets/gsj-reports.md) | 2誌のPDFの文字層を1ページ1行のJSONLにした49,065ページ、約2.6億字 | 386.1 MB | cc-by-4.0 |
| [mlit-river-basin-overviews](../datasets/mlit-river-basin-overviews.md) | 一級水系の流域の地形・地質・気候・土地利用・歴史・災害を述べた115文書、9,894ページ、約610万字のJSONL | 37.8 MB | other |
| [moni1000-reports](../datasets/moni1000-reports.md) | 73文書12,148ページ、約860万字のJSONL | 57.6 MB | other |
| [nilim-disaster-reports](../datasets/nilim-disaster-reports.md) | 国総研が単独で出し他の権利表記が無い26報告(883ページ)の本文JSONL | 4.5 MB | cc-by-4.0 |
| [rinya-forest-inventory](../datasets/rinya-forest-inventory.md) | 1文書3ページ、約2,900字のJSONL | 0.0 MB | other |
| [un-docs](../datasets/un-docs.md) | 39,363文書の本文 | 409.4 MB | other |
| [wikidata-gazetteer](../datasets/wikidata-gazetteer.md) | 座標(P625)かWikipedia記事数(P1566)を持つ全項目12,205,328件と、552言語の名前62,506,107件、行政階層 | 863.4 MB | cc0-1.0 |
| [wikipedia-geotagged](../datasets/wikipedia-geotagged.md) | 座標つき記事の本文 | 2.20 GB | cc-by-sa-4.0 |
| [wikivoyage-geotagged](../datasets/wikivoyage-geotagged.md) | 座標つきの英語版 Wikivoyage 記事29,505件(2.34億字) | 101.7 MB | cc-by-sa-4.0 |

### 旧作(2024年)（6件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [g-uc](../datasets/g-uc.md) | エピソード・サブタイトル・場所・人物・テキストの3,344行の日本語データ(2024-03) | 0.3 MB | （なし） |
| [onomatopoeia-ja](../datasets/onomatopoeia-ja.md) | 日本語オノマトペ5,060件(英訳と詳細) | 0.3 MB | mit |
| [onomatopoeia-ja-flat](../datasets/onomatopoeia-ja-flat.md) | オノマトペを平らにした10,346行(`text`・`text_lang`・`onomatopoeia_ja`) | 0.2 MB | （なし） |
| [open2ch-livejupiter-qa](../datasets/open2ch-livejupiter-qa.md) | おーぷん2ちゃんねる(ライブジュピター)の質問と回答663,546組 | 47.3 MB | （なし） |
| [sake_qa](../datasets/sake_qa.md) | 日本酒の質問応答5,176件(`input`・`output`・`type`) | 0.1 MB | mit |
| [scp-jp-plain](../datasets/scp-jp-plain.md) | SCP財団日本語版の本文999件 | 5.3 MB | cc-by-sa-3.0 |

### 北海道東部の窓抽出（6件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [ctrees-agb-hokkaido-east-100m](../datasets/ctrees-agb-hokkaido-east-100m.md) | 東部北海道の固定の長方形窓で、CTrees の地上部バイオマス（AGB）と不確かさを、10×10画素のブロックごとに集約した多角形（43,550件） | 27.9 MB | cc-by-4.0 |
| [forest-typology-validation-2020](../datasets/forest-typology-validation-2020.md) | ForTy 森林タイプ図の検証用の世界の標本9,100地点を点にした GeoParquet | 1.6 MB | cc-by-4.0 |
| [forty-hokkaido-east-2020](../datasets/forty-hokkaido-east-2020.md) | 6クラスの森林タイプ図（10m）の、東部北海道の6タイルを多角形化した GeoParquet（63,630件） | 20.5 MB | cc-by-4.0 |
| [gebco-2026-hokkaido-east-15as](../datasets/gebco-2026-hokkaido-east-15as.md) | GEBCO 2026（海陸の15秒格子）の北海道東方の3°×3°を、画素ごとの長方形の多角形（518,400件、720×720）と標高（m、負は水深）にした GeoParquet | 3.9 MB | other |
| [gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2](../datasets/gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2.md) | 正味フラックス（2001〜2023年の累積、Mg CO₂e/ha）が0でないセルの中心点を、点の GeoParquet（34,516,630行）にしたもの | 127.1 MB | cc0-1.0 |
| [gpw-grasslands-hokkaido-east-2018-2020-250m](../datasets/gpw-grasslands-hokkaido-east-2018-2020-250m.md) | 草地の優占クラス（耕作草地・自然半自然草地・低木地・その他）の30m図を、10×10画素のブロック（約250m）に集約した多角形（313,489件） | 13.3 MB | cc-by-4.0 |

### クマ出没記録（6件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [akita-kumadas-wildlife-sighting](../datasets/akita-kumadas-wildlife-sighting.md) | クマダスの目撃・痕跡・人身被害の記録24,757件（2022-04-10〜2026-09-30） | 8.5 MB | cc-by-4.0 |
| [gifu-bear-sighting](../datasets/gifu-bear-sighting.md) | ツキノワグマの目撃記録6,946件（FY2014〜FY2025）を年度ごと12表の GeoParquet にしたもの | 1.2 MB | cc-by-4.0 |
| [ishikawa-bear-incident](../datasets/ishikawa-bear-incident.md) | クマの出没データ3,901件を6表の GeoParquet にしたもの | 1.2 MB | cc-by-4.0 |
| [kamisunagawa-higuma-sighting](../datasets/kamisunagawa-higuma-sighting.md) | 北海道上砂川町のヒグマの出没105件（2024-05-11〜2026-08-19、R6〜R8） | 0.1 MB | cc-by-4.0 |
| [kyoto-bear-sighting](../datasets/kyoto-bear-sighting.md) | ツキノワグマの目撃10,225件（2009-04-08〜2018-12-10） | 2.7 MB | cc-by-4.0 |
| [nagaoka-bear-sighting](../datasets/nagaoka-bear-sighting.md) | 新潟県長岡市のクマの目撃・痕跡166件（平成26・27年度、2014-04-09〜2016-03-30） | 0.2 MB | cc-by-4.0 |

### 災害・気象（7件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [ibtracs-v04r01](../datasets/ibtracs-v04r01.md) | 世界の台風・ハリケーンなどの熱帯低気圧の観測位置311,935行（1980-01-01〜2026-10-22 UTC） | 154.0 MB | other |
| [ibtracs-v04r01-2026-10](../datasets/ibtracs-v04r01-2026-10.md) | 意図的に空のリポジトリで、カードは「IBTrACS v04r01 は yuiseki/ibtracs-v04r01 に置いてある（since1980 の GeoParquet）」と述べる | 0.0 MB | other |
| [jma-rain-tokyo](../datasets/jma-rain-tokyo.md) | 東京都内の気象庁31観測所の降水量（日別588,783観測所日、時別8,660,976観測所時）と、観測所一覧・取得ファイルの記録 | 282.3 MB | cc-by-4.0 |
| [ksj-a31a-flood-greater-tokyo](../datasets/ksj-a31a-flood-greater-tokyo.md) | 東京23区版（ksj-a31a-flood-tokyo23）を広げ、埼玉・千葉・東京・神奈川に触れる洪水浸水想定区域4,366,127件（5カテゴリ） | 4.21 GB | cc-by-4.0 |
| [ksj-a31a-flood-tokyo23](../datasets/ksj-a31a-flood-tokyo23.md) | 東京23区に触れる洪水浸水想定区域227,651件（計画規模50,124・想定最大規模136,671・浸水継続時間40,374・家屋倒壊等氾濫想定（氾濫流301・河岸浸食181）） | 1.47 GB | cc-by-4.0 |
| [tokyo-flood-record-jp](../datasets/tokyo-flood-record-jp.md) | 東京の浸水実績5,845区域（多角形）と121点（点）の、被害の棟数・世帯数・河川・区市町村・最寄りの雨量計の降雨を持つ記録 | 3.2 MB | cc-by-4.0 |
| [usgs-comcat-2025-m45](../datasets/usgs-comcat-2025-m45.md) | 2025年のマグニチュード4.5以上の地震8,502件（優先ネットワーク `us`、事象種別 earthquake） | 6.7 MB | other |

### 気候（3件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [agera5-japan-monthly-temperature-1979-2026](../datasets/agera5-japan-monthly-temperature-1979-2026.md) | 日本周辺の窓（長方形、海を含む）の0.1°格子の月別気温を、セルの中心点の GeoParquet（47,507,200行、571か月、年ごと48ファイル）にしたもの | 84.6 MB | cc-by-4.0 |
| [agera5-japan-monthly-water-1979-2026](../datasets/agera5-japan-monthly-water-1979-2026.md) | 日本周辺の窓の0.1°格子の月別降水量（`precip_mm`）と基準蒸発散量（`et0_mm`、いずれも月合計mm）を、セルの中心点の GeoParquet（47,507,200行、571か月、年ごと48ファイル）にしたもの | 71.9 MB | cc-by-sa-4.0 |
| [koppen-geiger-east-asia-1991-2020](../datasets/koppen-geiger-east-asia-1991-2020.md) | ケッペン・ガイガーの気候区分図を、同じクラスが4連結で続く領域の多角形（13,480件）にした GeoParquet | 13.5 MB | cc-by-4.0 |

### 人口・建物・土地被覆（6件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [esa-worldcover-tokyo-2021-100m](../datasets/esa-worldcover-tokyo-2021-100m.md) | 10m の土地被覆図を、10×10画素のブロック（約100m、360,000件）の多角形にし、11クラスの画素数・優占クラス・優占率を持たせた GeoParquet | 34.1 MB | cc-by-4.0 |
| [ghsl-japan-core-2020-30arcsec](../datasets/ghsl-japan-core-2020-30arcsec.md) | 2020年の居住人口（GHS-POP）と建物表面積（GHS-BUILT-S）を、各720万セルの多角形にした GeoParquet（5タイル×2種、合計1,440万行） | 177.7 MB | cc-by-4.0 |
| [kontur-population-2023-11-01-22km](../datasets/kontur-population-2023-11-01-22km.md) | 世界を H3 解像度4（約22km）のセルにした人口の推定（71,283セル） | 10.2 MB | other |
| [microsoft-building-footprints-kanto-2026-08-13](../datasets/microsoft-building-footprints-kanto-2026-08-13.md) | 東京・東関東の2つの QuadKey の機械検出の建物の多角形5,781,554件（`height`・`confidence`・`quadkey`） | 840.2 MB | other |
| [worldpop-idn-population-2015-2030-1km-r2025a](../datasets/worldpop-idn-population-2015-2030-1km-r2025a.md) | WorldPop の2015〜2030年の年次人口推定（制約つき）を、1km の元の格子のセル多角形にした GeoParquet（948,911セル） | 94.3 MB | other |
| [worldpop-kor-population-2015-2030-1km-r2025a](../datasets/worldpop-kor-population-2015-2030-1km-r2025a.md) | WorldPop の2015〜2030年の年次人口推定を、韓国の1km 格子のセル多角形にした GeoParquet（130,927セル | 12.9 MB | other |

### 地形・基盤（2件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [gsi-dem-fuji-z14-100m-2026-10-25](../datasets/gsi-dem-fuji-z14-100m-2026-10-25.md) | 国土地理院の DEM10B の標高タイル100枚（ズーム14、10×10）を、10×10画素ごとの約100m の Web Mercator 格子にして、平均・最小・最大標高と有効画素数を持たせた GeoParquet（65,536セル） | 52.5 MB | other |
| [timezone-boundary-builder-2026d](../datasets/timezone-boundary-builder-2026d.md) | タイムゾーンの境界の多角形（`tzid` つき）を3つの設定（全ゾーン、1970年以降同じ、現在同じ）の GeoParquet にしたもの | 333.9 MB | odbl |

### 東北6県の森林資源・植生（12件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [akita-forest-resource-mesh-2026](../datasets/akita-forest-resource-mesh-2026.md) | 秋田県の陸地の20mメッシュ29,088,595セル（60シート、シートの計38,875,524セルから秋田県の分を切り出し）を、シートごとの GeoParquet にしたもの（EPSG:6678） | 277.5 MB | other |
| [akita-vegetation-2024](../datasets/akita-vegetation-2024.md) | 秋田県の現存植生図2024を切り出した GeoParquet（174,576ポリゴン、11,635.9 km²） | 235.0 MB | other |
| [aomori-forest-resource-mesh-2026](../datasets/aomori-forest-resource-mesh-2026.md) | 青森県の陸地の20mメッシュ24,108,678セル（63シート、シートの計29,837,059セルから青森県の分を切り出し）を、シートごとの GeoParquet にしたもの（EPSG:6678） | 236.8 MB | other |
| [aomori-vegetation-2024](../datasets/aomori-vegetation-2024.md) | 青森県の現存植生図2024を切り出した GeoParquet（147,302ポリゴン、9,643.5 km²） | 139.8 MB | other |
| [fukushima-forest-resource-mesh-2026](../datasets/fukushima-forest-resource-mesh-2026.md) | 福島県の陸地の20mメッシュ34,452,709セル（69シート、シートの計39,939,045セルから福島県の分を切り出し）を、シートごとの GeoParquet にしたもの（EPSG:6677） | 335.1 MB | other |
| [fukushima-vegetation-2024](../datasets/fukushima-vegetation-2024.md) | 福島県の現存植生図2024を切り出した GeoParquet（336,047ポリゴン、13,781.0 km²） | 323.1 MB | other |
| [iwate-forest-resource-mesh-2026](../datasets/iwate-forest-resource-mesh-2026.md) | 岩手県の陸地の20mメッシュ38,179,256セル（72シート、シートの計46,980,617セルから岩手県の分を切り出し）を、シートごとの GeoParquet にしたもの（EPSG:6678） | 344.1 MB | other |
| [iwate-vegetation-2024](../datasets/iwate-vegetation-2024.md) | 岩手県の現存植生図2024を切り出した GeoParquet（248,187ポリゴン、15,271.8 km²） | 204.3 MB | other |
| [miyagi-forest-resource-mesh-2026](../datasets/miyagi-forest-resource-mesh-2026.md) | 宮城県の陸地の20mメッシュ18,194,823セル（47シート、シートの計26,280,216セルから宮城県の分を切り出し）を、シートごとの GeoParquet にしたもの（EPSG:6678） | 181.6 MB | other |
| [miyagi-vegetation-2024](../datasets/miyagi-vegetation-2024.md) | 宮城県の現存植生図2024を切り出した GeoParquet（143,044ポリゴン、7,278.0 km²） | 129.3 MB | other |
| [yamagata-forest-resource-mesh-2026](../datasets/yamagata-forest-resource-mesh-2026.md) | 山形県の陸地の20mメッシュ23,319,199セル（53シート、シートの計30,267,408セルから山形県の分を切り出し）を、シートごとの GeoParquet にしたもの（EPSG:6678） | 230.9 MB | other |
| [yamagata-vegetation-2024](../datasets/yamagata-vegetation-2024.md) | 山形県の現存植生図2024を切り出した GeoParquet（141,922ポリゴン、9,327.7 km²） | 162.3 MB | other |

### ブナの豊凶（2件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [fagus-crenata-masting-jp-2026-06](../datasets/fagus-crenata-masting-jp-2026-06.md) | ブナの種子生産の調査データ（東北98地点と北海道渡島半島4地点、1989〜2008年）の凍結コピー | 1.2 MB | cc0-1.0 |
| [landsat5-fagus-crenata-sites-jp-2026-10](../datasets/landsat5-fagus-crenata-sites-jp-2026-10.md) | ブナの豊凶データの102地点（東北98・渡島4）の周辺300m以内について、1989〜2008年の4〜5月と7〜8月の全ての Landsat 5 の撮影から、地表反射率とQAを抽出した表 | 44.9 MB | other |

### 気象・地球物理の原本（3件）

| データセット | 中身 | 全体 | ライセンスタグ |
|---|---|---|---|
| [igrf-14-coefficients-2024-11](../datasets/igrf-14-coefficients-2024-11.md) | IGRF-14 のシュミット準正規化球面調和係数（次数1〜13、1900〜2025年の26時点と、2025〜30年の永年変化） | 0.1 MB | other |
| [ncep-cpc-global-ir-4km-2026-10](../datasets/ncep-cpc-global-ir-4km-2026-10.md) | 静止気象衛星の約11µm赤外の輝度温度を全球（60°N〜60°S）で合成した4km格子の、1時間ごとのファイル168個（各ファイルに:00と:30の2枚）を、配布されたままの圧縮ファイル（.Z）で凍結したもの（4.55GB） | 4.55 GB | other |
| [ncep-ncar-reanalysis1-air-sig995-2026-03](../datasets/ncep-ncar-reanalysis1-air-sig995-2026-03.md) | NCEP/NCAR 再解析1の地表付近（シグマ0.995面）の気温の NetCDF（年ごと79ファイル、1948年〜2026-03-17）を、配布されたままで凍結したもの（約1.7GB） | 1.74 GB | other |

## 確かめなかったこと

- 分類の境界は便宜的（geo-triples-jp-gov は入力が jp-admin なので日本の公的データに置き、geo-triples-japan・tokyo23 は入力が OSM なので OSM の派生に置いた）。
- 一覧の「中身」は各データセットの踏み跡の要点の最初の1文。

## 出典

- Hugging Face API（2026-10-26）、各データセットのカード
