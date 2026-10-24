---
id: yuiseki-datasets-version-policies
title: 版の持ち方の4つの型：凍結、上書きの最新1回、版を積む、更新が止まったもの
status: draft
sources:
  - yuiseki/ 配下の各データセットのカード（Hugging Face 上の main、2026-10-24 取得）。個別の踏み跡の出典を参照
  - Hugging Face API（ファイル一覧、最終更新、コミット）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-scale
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-rights-exclusions
verified_how: read-docs
pattern: categories
finding:
  - 同じ yuiseki のデータセットでも「いつの値か」の意味が4通りある。引用するときは、型・取得日・コミットを添える必要がある
---

## 要点

- 元の配布元が値を直すかどうかと、写しを何回分持つかで、版の意味が決まる。個別のカードの「The data follows upstream corrections」「Why dated snapshots」「Why a frozen copy exists」などの節がこれを説明している。
- Hugging Face のコミット（sha）は、ファイルの版を固定する。ただし「上書きの最新1回」の型では、sha が変わると中身が置き換わる（旧版は残らないとカードが書く）。

## 4つの型

| 型 | 意味 | 該当するデータセット（カードの記述による） |
|---|---|---|
| A 凍結 | ある日・ある版の配布物を固定。名前に日付や版を持つことが多い | abr-src-2026-09、estat-boundary-2020、jp-admin-2026-09、osm-japan-src-2026-08、osm-tokyo23-src-2026-08、geo-triples-*、osm-tokyo23-*、ne-admin0-10m（5.1.1）、ourairports-2026-08、nfgis-2024、mlit-toshi-keikaku-jp（令和7年度）、ksj-n07-*・ksj-p11-*（2022年版）、mlit-underpass（R7.3.31）、mlit-1km-fromto-2022-01、estat-census-mesh-*（2026-10-11/13 取得） |
| B 上書きの最新1回 | 元が同じ名前で上書きし、写しは最新の1回だけを置いて、再取得で全体を置き換える | estat-jumin-idou、undata-sdmx、ilostat、faostat、ksj-l01-land-price（元の訂正を反映）、gsi-evacuation-sites-jp（毎朝更新の元） |
| C 版を積む | 日付や版ごとにサブセットを足していく | geonames（夜ごと）、opencellid（日付ごと）、worldbank-wdi（7版）、pwt（8.0〜11.0）、maddison-project（3版）、un-wpp（1998〜2024）、ucdp-ged（19.1〜26.1）、undp-hdr、unhcr-refugee-stats、ekidata-jp、env-redlist-jp、gsi-global-map-jp（3版）、natural-earth（レイヤーごとの版）、meta-move-dist（日ごと） |
| D 更新が止まったもの | 元が更新を終えた | meta-range-maps-2022-05（2022-05-22 で終了）、natural-earth（2022年5月から無更新）、旧作6件（2024年3〜4月） |

## 使うときの注意（意味づけ）

- **型 B の引用**: 日付を添えなければ再現できない。sha を固定しても、再取得後は同じ sha の中身が変わるわけではないが、「最新を指すリンク」は将来別の中身になる。
- **型 C の結合**: 版をまたいで積むと、定義が変わっている（pwt のリリース間、maddison-project の3版は積めないとカードが書く）。積む前に定義を確認する。
- **型 A でもカードより新しい**: jp-admin-2026-09 は、カード（2026-09-28 時点）では GeoParquet メタデータが無かったが、2026-10-06 更新の HEAD では GeoParquet 1.1 になっていた。型 A でも、main が動くことがある。
- **元が訂正する**: ksj-l01-land-price の元サイトは、訂正のたびに同じファイルを上書きする。

## 確かめなかったこと

- 型の割り当ては、カードの記述に基づく。全データセットで元配布元の挙動を独立には確認していない。
- 型 A の「凍結」が、main のコミットが動かないことまで意味するかは確認していない（jp-admin の例では動いた）。

## 出典

- 各データセットのカード（個別の踏み跡の出典欄を参照）
- Hugging Face API（2026-10-24）
