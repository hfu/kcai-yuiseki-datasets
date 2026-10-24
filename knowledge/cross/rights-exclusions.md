---
id: yuiseki-datasets-rights-exclusions
title: 権利を理由に除かれたもの：どのデータセットで、何が、なぜ含まれていないか
status: draft
sources:
  - yuiseki/ 配下の各データセットのカード（Hugging Face 上の main、2026-10-24 取得）。個別の踏み跡の出典を参照
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-version-policies
  - yuiseki-datasets-scale
verified_how: read-docs
pattern: practice
finding:
  - 多くの統計・国際機関系データセットは、CC BY で再配布できない部分をあらかじめ除いている。「元の全量」ではなく「再配布できる部分」だと理解して使う必要がある
---

## 要点

- yuiseki のデータセットは、元の配布物をできるだけそのまま保つ一方、権利の面で CC BY 4.0（またはそれと互換）で配れない部分は含めない方針を取っている。除外の基準と対象はカードに書かれ、MANIFEST にも残るものが多い。
- 利用側で「全量だと思って結論を出す」と、欠けた部分に気づかない。

## 除外の一覧（カードの記述）

| データセット | 除かれたもの | 理由（カードの記述） |
|---|---|---|
| worldbank-wdi | 74指標（SIPRI 軍事支出、IEA エネルギー、WDPA 保護地域など） | いずれかの版で CC BY 以外か空と表示。版ごとにラベルが変わるため全版から除外。世界銀行の zip も置かない |
| faostat | 廃止系列3つ（食料援助、世帯調査指標、旧生産者価格） | 更新日が2019-11-30（CC BY 適用）より前 |
| ilostat | 公表が2023-05-03より前の指標ファイル | ILO が CC BY を適用するのは2023-05-03以降の公表分 |
| edgar-ghg-countries | 化石CO2（IEA-EDGAR CO2）と、それを含む合計 | CC BY-NC-ND 4.0 |
| undata-sdmx | NA_MAIN の IMF 作成行と Eurostat のコソボ行（61,921行） | 作成機関が再配布を認めない |
| un-statistical-yearbook | WHO、ITU、IMF、IUCN、UNODC、UN Tourism、WIPO、IPU、UNEP-WCMC の行 | 出典機関の規約で再配布不可（UIS は CC BY-SA 4.0）。22表105,902行のみ |
| unhcr-refugee-stats | 第三者（IDMC、UNRWA）のデータ | UNHCR のものでない |
| nilim-disaster-reports | 共同刊行・共著・判断不能の118報告 | 他機関の権利が及ぶ。理由を EXCLUDE.txt、RIGHTS_REVIEW.tsv に記録 |
| ksj-n07-*、ksj-p11-* | 2011年版・2010年版 | 非商用の条件 |
| natural-earth | ラスタ（約7.5GB） | 容量。権利ではない |

## 権利や出典の扱いが条件つきのもの（含まれているが注意）

- ucdp-ged: `source_*` 列に報道の見出しの引用。見出しを UCDP が再許諾できるかは未確認とカードが述べる。
- mlit-river-basin-overviews、moni1000-reports: 地方整備局・都道府県・他者のクレジットが混じりうるが、個別確認はされていない。
- opencellid、wikipedia-geotagged、wikivoyage-geotagged、scp-jp-plain: CC BY-SA（継承）。
- OSM 系（osm-*、geo-triples-japan、geo-triples-tokyo23、text2geoql、osm-wikidata-brand-*）: ODbL（share-alike）。同じ日本の行政区画でも、jp-admin・estat-boundary・abr-src・geo-triples-jp-gov は CC BY 系で、ここが分かれ目だとカードが説明している。
- ekidata-jp: 無改変であれば無償再配布が可能、という条件。

## 使うときの注意（意味づけ）

- 「WDI の全指標」「FAOSTAT の全ドメイン」として扱えない。必要な系列が除外対象かを MANIFEST で確認する。
- 派生物を作って再配布するときは、継承（ODbL・CC BY-SA）の有無を先に確認する。日本の行政区画では、継承の無い系列（jp-admin など）を起点にすると組み立てやすい。

## 確かめなかったこと

- 各除外の判断が法的に妥当かどうかは確認していない（カードの記述のとおり）。
- 除外が MANIFEST と一致しているかを、全データセットで照合してはいない。

## 出典

- 各データセットのカード（個別の踏み跡の出典欄を参照）
