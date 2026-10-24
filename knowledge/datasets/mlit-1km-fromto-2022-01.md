---
id: mlit-1km-fromto-2022-01
title: mlit-1km-fromto-2022-01 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/mlit-1km-fromto-2022-01 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 2424a9d、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - estat-census-mesh-2020
  - meta-move-dist
dataset: yuiseki/mlit-1km-fromto-2022-01
verified_how: read-data
pattern: questions
finding:
  - 1kmメッシュごとの月別平均滞在人口と、居住地別の市区町村間流動(平日/休日、昼/深夜)
---

## 要点

- 1kmメッシュごとの月別平均滞在人口と、居住地別の市区町村間流動(平日/休日、昼/深夜)。元 zip 99本と Parquet 5本(メッシュ別3,808万行)。
- 分類: 日本の統計・公的GIS。元の情報源: 国土交通省「全国の人流オープンデータ」(2019-01〜2021-12)。
- 権利: 政府標準利用規約 2.0(CC BY 4.0 互換)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 2424a9d（最終更新 2026-10-01、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 317.3 MB、ファイル 109 本 |
| Parquet | 5 本、合計 116.6 MB、最大 104.1 MB |
| 行数 | 41,199,373（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/monthly_mdp_mesh1km.parquet`） | 8（うち文字列 7） |
| 行グループ数（標本の最大） | 380 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: monthly_mdp_mesh1km.parquet、regioncode_master.parquet。他のファイルは未検査） |

## 答えうる問い

- 月別・時間帯別の滞在人口のメッシュ分布
- 居住地市区町村ごとの流動

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| キー | コードは文字列(`prefcode` が '01'、`citycode` が '01101')で桁落ちしない | — |
| 版 | — | 属性表と2つのマスターに2019年版と2020年版があり、`version` 列で区別する。1つに絞って結合しないと行が倍になる |
| コード | — | 2019年版では福岡県の中川市がまだ旧町のコード40305を持つ(定義書の注記どおり) |
| 型 | — | `population` 以外は全列が文字列 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- ファイルの日付(公開日)と中身の期間のずれはカード参照。ここでは未検証

## 出典

- yuiseki/mlit-1km-fromto-2022-01 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/mlit-1km-fromto-2022-01?blobs=true`）と Parquet フッターの取得（2026-10-24）
