---
id: mlit-toshi-keikaku-jp
title: mlit-toshi-keikaku-jp で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/mlit-toshi-keikaku-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 39fdb22、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - jp-admin-2026-09
  - estat-boundary-2020
dataset: yuiseki/mlit-toshi-keikaku-jp
verified_how: read-data
pattern: questions
finding:
  - 約1,400市区町村の都市計画決定(用途地域・都市計画道路・公園・地区計画・立地適正化計画など)
---

## 要点

- 約1,400市区町村の都市計画決定(用途地域・都市計画道路・公園・地区計画・立地適正化計画など)。レイヤー別26本の GeoParquet と、Shapefile/GeoJSON/CityGML の元 zip。
- 分類: 日本の統計・公的GIS。元の情報源: 国土交通省 都市局「都市計画決定GISデータ」令和7年度版(2026-05-21公開、同年7月訂正)。
- 権利: 国交省の利用規約(PDL1.0、CC BY 4.0 互換)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 39fdb22（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 2.65 GB、ファイル 177 本 |
| Parquet | 26 本、合計 626.4 MB、最大 134.5 MB |
| 行数 | 424,335（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/fy2025/youto.parquet`） | 16（うち文字列 12） |
| 行グループ数（標本の最大） | 2 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `ValidType` 99.8%、`INNumber` 99.3%、`INDate` 99.0%、`Custodian` 98.7% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 用途地域・容積率・建蔽率の分布
- 都市計画道路・公園などの整備状況を自治体ごとに比べる

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何・座標系 | GeoParquet。CRS は EPSG:6668(JGD2011)。Shapefile の `.cpg` は UTF-8 で、文字コードの問題が起きにくい | — |
| 検証 | 元 DBF の全属性値(4,967,475)と一致するとカードが検証 | — |
| 網羅性 | — | 自治体が提出したものだけ。自治体一覧の〇×と実ファイルは一致しない(道路: 一覧834に対しファイル785)。件数は一覧でなくデータから数える |
| 空のジオメトリ | — | 道路5,802行(3自治体)ほかに null の形がある(属性は残る) |
| コード | — | YoutoCode 0 / 調整(茅ヶ崎)など定義に無い値が6行 |
| 規模 | — | 合計2.65GB。レイヤーにより最大約135MB |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/mlit-toshi-keikaku-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/mlit-toshi-keikaku-jp?blobs=true`）と Parquet フッターの取得（2026-10-24）
