---
id: yuiseki-datasets-growth-2026-10-26
title: yuiseki のデータセットの増え方：2日で69件から96件へ、新規27件の概観
status: draft
sources:
  - Hugging Face API `/api/datasets?author=yuiseki`（2026-10-24 と 2026-10-26 の比較）
  - 新規27件のデータセットカード（Hugging Face 上の main、2026-10-26 取得）
  - 新規27件の Parquet のフッター（2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - yuiseki-datasets-index
  - yuiseki-datasets-scale
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-version-policies
verified_how: read-data
pattern: landscape
finding:
  - 2026-10-24 から 2026-10-26 の2日で27件が増えた。新規の地物系26件はすべて GeoParquet の `geo` メタデータを持つが、bbox の covering は一件も無い。作り方は、スクリプト・テスト・ロックファイルを同梱した再現可能な小さなプロジェクトに変わっている
---

## 要点

- 2026-10-24 に 69 件だった yuiseki のデータセットが、2026-10-26 に **96 件**になった（削除は無し。既存69件のコミットは変わっていない）。増えた27件の更新日はすべて 2026-10-25〜26。合計 3.78 GB。
- 新規27件の個別の踏み跡は `knowledge/datasets/<名前>.md` に作成した（2026-10-26）。索引（`yuiseki-datasets-index`）は96件に更新、規模（`yuiseki-datasets-scale`）には追加分の表を足した。この文書は概観。

## 新規27件（主題ごと）

### 北海道東部の森林・草地・地形（窓で切った抽出）（6件）

| データセット | 更新 | 全体 | 行数 | 行グループ | `geo`（版 / covering） | ライセンスタグ |
|---|---|---|---|---|---|---|
| ctrees-agb-hokkaido-east-100m | 2026-10-25 | 27.9 MB | 43,550 | 1 | 1.0.0 / なし | cc-by-4.0 |
| forty-hokkaido-east-2020 | 2026-10-25 | 20.5 MB | 63,630 | 11 | 1.0.0 / なし | cc-by-4.0 |
| gebco-2026-hokkaido-east-15as | 2026-10-25 | 3.9 MB | 518,400 | 17 | 1.1.0 / なし | other |
| gfw-forest-carbon-net-flux-hokkaido-east-2001-2023-v1-3-2 | 2026-10-25 | 127.1 MB | 34,516,630 | 47 | 1.1.0 / なし | cc0-1.0 |
| gpw-grasslands-hokkaido-east-2018-2020-250m | 2026-10-25 | 13.3 MB | 313,489 | 1 | 1.1.0 / なし | cc-by-4.0 |
| forest-typology-validation-2020 | 2026-10-25 | 1.6 MB | 17,290 | 5 | 1.0.0 / なし | cc-by-4.0 |

### クマの出没記録（自治体のオープンデータ）（6件）

| データセット | 更新 | 全体 | 行数 | 行グループ | `geo`（版 / covering） | ライセンスタグ |
|---|---|---|---|---|---|---|
| akita-kumadas-wildlife-sighting | 2026-10-26 | 8.5 MB | 24,757 | 1 | 1.1.0 / なし | cc-by-4.0 |
| gifu-bear-sighting | 2026-10-26 | 1.2 MB | 6,946 | 1 | 1.1.0 / なし | cc-by-4.0 |
| ishikawa-bear-incident | 2026-10-26 | 1.2 MB | 3,901 | 1 | 1.1.0 / なし | cc-by-4.0 |
| kamisunagawa-higuma-sighting | 2026-10-26 | 0.1 MB | 105 | 1 | 1.1.0 / なし | cc-by-4.0 |
| kyoto-bear-sighting | 2026-10-26 | 2.7 MB | 10,225 | 1 | 1.1.0 / なし | cc-by-4.0 |
| nagaoka-bear-sighting | 2026-10-26 | 0.2 MB | 166 | 1 | 1.1.0 / なし | cc-by-4.0 |

### 水害・降雨・地震・台風（5件）

| データセット | 更新 | 全体 | 行数 | 行グループ | `geo`（版 / covering） | ライセンスタグ |
|---|---|---|---|---|---|---|
| tokyo-flood-record-jp | 2026-10-26 | 3.2 MB | 5,966 | 1 | 1.1.0 / なし | cc-by-4.0 |
| ksj-a31a-flood-tokyo23 | 2026-10-26 | 1.47 GB | 455,302 | 5 | 1.1.0 / なし | cc-by-4.0 |
| jma-rain-tokyo | 2026-10-26 | 282.3 MB | 9,250,809 | 9 | なし（表） | cc-by-4.0 |
| ibtracs-v04r01 | 2026-10-25 | 154.0 MB | 311,935 | 7 | 1.0.0 / なし | other |
| usgs-comcat-2025-m45 | 2026-10-25 | 6.7 MB | 8,502 | 5 | 1.0.0 / なし | other |

### 気候・気象（2件）

| データセット | 更新 | 全体 | 行数 | 行グループ | `geo`（版 / covering） | ライセンスタグ |
|---|---|---|---|---|---|---|
| agera5-japan-monthly-temperature-1979-2026 | 2026-10-25 | 84.6 MB | 47,507,200 | 12 | 1.1.0 / なし | cc-by-4.0 |
| koppen-geiger-east-asia-1991-2020 | 2026-10-25 | 13.5 MB | 13,480 | 3 | 1.0.0 / なし | cc-by-4.0 |

### 人口・建物・土地被覆（6件）

| データセット | 更新 | 全体 | 行数 | 行グループ | `geo`（版 / covering） | ライセンスタグ |
|---|---|---|---|---|---|---|
| ghsl-japan-core-2020-30arcsec | 2026-10-25 | 177.7 MB | 14,400,000 | 15 | 1.0.0 / なし | cc-by-4.0 |
| kontur-population-2023-11-01-22km | 2026-10-25 | 10.2 MB | 71,283 | 7 | 1.0.0 / なし | other |
| worldpop-idn-population-2015-2030-1km-r2025a | 2026-10-25 | 94.3 MB | 948,911 | 33 | 1.1.0 / なし | other |
| worldpop-kor-population-2015-2030-1km-r2025a | 2026-10-25 | 12.9 MB | 130,927 | 11 | 1.1.0 / なし | other |
| microsoft-building-footprints-kanto-2026-08-13 | 2026-10-25 | 840.2 MB | 5,781,554 | 392 | 1.0.0 / なし | other |
| esa-worldcover-tokyo-2021-100m | 2026-10-25 | 34.1 MB | 360,000 | 8 | 1.0.0 / なし | cc-by-4.0 |

### 地形・基盤（2件）

| データセット | 更新 | 全体 | 行数 | 行グループ | `geo`（版 / covering） | ライセンスタグ |
|---|---|---|---|---|---|---|
| gsi-dem-fuji-z14-100m-2026-10-25 | 2026-10-25 | 52.5 MB | 65,536 | 1 | 1.1.0 / なし | other |
| timezone-boundary-builder-2026d | 2026-10-25 | 333.9 MB | 785 | 1 | 1.0.0 / なし | odbl |

## 新規の作りの特徴（カードとフッターから）

- **主題が変わった。** 既存は国・全国規模の公的データと国際機関の統計が中心だったが、新規は(1)北海道東部（経度 142〜147 度、緯度 42〜46 度付近）の窓で切った森林・草地・地形、(2)クマの出没記録（秋田・岐阜・石川・京都・長岡・上砂川、いずれも自治体のオープンデータ）、(3)東京の水害・降雨、(4)人口・建物の格子、が目立つ。特定の地域・主題を切り出した小さなデータセットが増えている。
- **ラスタをベクタ（GeoParquet）にしている。** 多くは、ラスタ（GeoTIFF）のセルや 10×10 画素のブロックを多角形や点にして保持する。例: esa-worldcover-tokyo（10m を 100m ブロックにして360,000セル）、gebco（15秒の画素ごとの多角形518,400）、ghsl（30秒、7,200,000セル×2種）、gfw（セルの中心点 34,516,630）。元のラスタは `source/` に併置するものと、再配布しないもの（WorldPop）がある。
- **`geo` メタデータは標準になった。** 地物を持つ26件はすべて GeoParquet の `geo` を持つ（1.1.0 が15件、1.0.0 が11件）。`jma-rain-tokyo` は幾何の無い表。一方、**bbox の covering を持つものは0件**。前の実験（estat-boundary-2020）では、bbox 列と空間順の行グループが無いと terrio-js の範囲読みは効かなかったので、新規のファイルも同じ条件では全量読みになると見込まれた。測ると、11本中9本は全量（約100%）、gfw は約73%、worldpop-idn は約14%だった。
- **点の CRS は書かれない。** クマの出没記録など点のファイルの多くは `crs` を書かない（GeoParquet の既定は WGS 84 相当）。座標が WGS 84 経緯度かどうかは、カードの記述による。
- **再現可能な小さなプロジェクトになった。** `pyproject.toml`、`uv.lock`、`scripts/01_download.py`〜`04_publish.py`、`src/`、`tests/`、`source/MANIFEST.json`（URL・バイト数・SHA-256）、`VERIFICATION.json` を同梱するものが多い（例: ctrees-agb、esa-worldcover、worldpop-idn）。既存のデータセットでは、検証は別のソースリポジトリの `scripts/02_verify.py` に置かれていた。
- **ライセンスの書き方が増えた。** タグが `other` のもの（gebco: OGL v3.0 と GEBCO の条件、microsoft-building-footprints: CDLA-Permissive-2.0、ibtracs、kontur、usgs-comcat、gsi-dem-fuji、worldpop-idn/kor）がある。worldpop-idn/kor のメタデータ名は `odbl-1.0-worldpop-cc-by-4.0-source` で、既存の worldpop-jp-2026-01（CC BY 4.0）と書き方が違う。理由は読んでいない（未確認）。
- **規模は小さいものが多い。** 27件中、全体が 100MB 未満のものが多数。大きいのは ksj-a31a-flood-tokyo23（1.47 GB。元 zip が約1.26GB）、microsoft-building-footprints（840.2 MB、578万棟、QuadKey ごとに392行グループ）、jma-rain-tokyo（282.3 MB、CSV が1,019本）。

## 既存の踏み跡との関係

- `yuiseki-datasets-version-policies` の型では、新規は型 A（凍結：日付やコミットを名前や内容に固定）が中心。jma-rain-tokyo は、初出の名前 `jma-tokyo-daily-rain` から改名されたとカードにある。
- `yuiseki-datasets-code-systems` に足す候補: 気象庁の都府県番号（東京は44）、クマの出没記録の自治体ごとの列名・年度表記の違い（岐阜は年度ごとの12表、石川は原因別の5表と年ごとの1表）。
- 既存の estat-boundary-2020 の問題（`geo` メタデータ無し）は、新規では起きていない。作り方が改善された例として参照できる。

## 確かめなかったこと

- 新規の範囲読みは、terrio-js 0.4.2 で11本を測った（`checks/check-2026-10-26-new-geoparquet-range-reads.md`）。DuckDB と terrio CLI は未実施。
- 個別の踏み跡の全行の文字検査は、データセットごとに最大1ファイル（130MB以下）まで。文字列の列を持つ主な表で、U+FFFD は ishikawa-bear-incident の `remarks`（2,423行中17）のみで見つかった。
- クマの出没記録の各自治体の列の意味、年度の違い、重複の有無は、カードを部分的に読んだのみ。
- 増えた理由や今後の方針は不明（Yuiseki さんの意図は読んでいない）。

## 出典

- Hugging Face API（2026-10-24、2026-10-26）、新規27件のカード、Parquet のフッター
