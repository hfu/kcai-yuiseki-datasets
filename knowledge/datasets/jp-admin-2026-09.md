---
id: jp-admin-2026-09
title: 市区町村コードと境界の基盤データ（jp-admin-2026-09）で何が答えられるか
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/jp-admin-2026-09.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - estat-boundary-2020
  - yuiseki-datasets-japan-admin-lineage
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-scale
dataset: yuiseki/jp-admin-2026-09
verified_how: read-card
pattern: questions
finding:
  - jp-admin は「名前とコードは abr-src（2026-09）、ポリゴンと人口は estat-boundary-2020（2020 年）」から作られた派生物で、1 行 1 市区町村の結合の起点に向く。政令市は本体と区が両方行になる
---

## 要点

- 47 都道府県（prefectures.parquet）と 1,918 市区町村（municipalities.parquet、政令市の区 171 を含む）。コード、漢字・かな・ローマ字の名前、代表点、2020 年の人口・世帯数、ポリゴンを 1 行に持つ。
- 名前とコードは abr-src-2026-09、ポリゴンと人口は estat-boundary-2020 から作られ、provenance.yaml が入力をコミット（3677b24、823195c）で固定している。だから、この 2 つと「別の独立なデータ」としてつなぐのではなく、派生関係として扱う。
- 出典のカードによる実測: lg_code と code5 は 1,918 通りで重複なし。人口の合計は ward が NULL の行で 126,146,099（区と市を両方足すと 153,154,439 で二重計上）。

## 答えうる問い

- 市区町村ごとの人口・世帯数・代表点を、6 桁の `lg_code` か 5 桁の `code5` で表にする。
- 都道府県ごとの市区町村数・人口を集計する（prefectures の municipalities 列の合計は 1,747＝1,918−171）。
- 市区町村の隣接を調べる（geo-triples-jp-gov の `sfTouches` が既にある。入力は jp-admin の 1,909 件）。

## 答えられない・気をつける問い

- 2024-01-01 新設の浜松市の 3 区（中央区、浜名区、天竜区）は名前だけで人口が NULL。北方領土の 6 村も人口 NULL（9 行）。浜松市本体は 2020 年の 7 区から作った形。
- 北方領土 6 村の代表点はすべて同じ点（経度 145.582903、緯度 43.330036）。距離を測る用途では外す。
- 小地域（町丁・字等）の問いには粗い。小地域は estat-boundary-2020 を使う。
- カードはポリゴンの型と範囲を未確認とし、CRS はファイルに無いとしていた（2026-09-28 時点）。HEAD（e6c87b1、2026-10-06 更新）では下記のとおり変わっている。

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

確かめた版: HEAD e6c87b1（2026-10-06 更新。カードを読んだ時点の 2026-09-26 版より新しい）。terrio 0.4.2、duckdb。

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何・座標系 | GeoParquet 1.1。`geo` メタデータあり（MultiPolygon/Polygon、`bbox` covering、CRS は EPSG:4612）。terrio 0.4.2 は `MultiPolygon`、1,918、`EPSG:4612` と認識した | カードの「geo メタデータは無い」は HEAD では古い。引用するときは sha を添える |
| 文字コード | 日本語（`香川県`、`高松市`）とローマ字が正しい。`lg_code` `372013` の先頭のゼロも保たれている（terrio で香川 17 件を GeoJSON に変換して確認） | なし（確かめた範囲） |
| 型 | population、households は BIGINT、代表点は DOUBLE で、そのまま数値として使える。コードは VARCHAR | 人口が NULL の 9 行（北方領土 6 村、浜松市の新 3 区）がある |
| 規模・分割 | municipalities は 47 の行グループ（最大 195 行）で、`bbox` 列つき。範囲で県ごとに絞れる作り | 1 本が 148.6 MB、prefectures も約 80 MB。terrio CLI のリモート読みは全量取得になる可能性が高い（0.3.2 の記録。jp-admin では未測定） |
| 意味 | 名前とコードは 2026-09 時点、人口は 2020 年で、現在の市区町村の表として使える | 時点が混在し、政令市は本体と区が両方行にある（人口は ward が NULL の行で取る）。北方領土 6 村の代表点は同一点 |

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/jp-admin-2026-09.md（コミット 6880b32）
