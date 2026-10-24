---
id: undata-sdmx
title: undata-sdmx で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/undata-sdmx のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット d4675c3、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - un-statistical-yearbook
  - edgar-ghg-countries
dataset: yuiseki/undata-sdmx
verified_how: read-data
pattern: questions
finding:
  - エネルギー統計・エネルギーバランス・国民経済計算の主要集計・SEEA(大気排出とエネルギー)の5データフロー、539万観測
---

## 要点

- エネルギー統計・エネルギーバランス・国民経済計算の主要集計・SEEA(大気排出とエネルギー)の5データフロー、539万観測。上書き型で最新の1回分。
- 分類: 世界の統計。元の情報源: UNdata SDMX API(国連統計部、2026-10-06取得)。
- 権利: UNdata の規約と作成機関の規約。IMF 作成行と Eurostat のコソボ行(NA_MAIN の61,921行)は除外。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d4675c3（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 514.9 MB、ファイル 691 本 |
| Parquet | 8 本、合計 16.0 MB、最大 5.9 MB |
| 行数 | 5,406,540（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/NA_MAIN.parquet`） | 40（うち文字列 36） |
| 行グループ数（標本の最大） | 16 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `EMBARGO_DATE` 100.0%、`COMMENT_TS` 100.0%、`TITLE_COMPL` 100.0%、`DATA_COMP` 100.0% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 国別のエネルギー供給・消費、排出と経済活動の対応

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | 観測数が API の申告値と一致、全737原本ファイルのハッシュ検証 | — |
| 権利除外 | — | NA_MAIN は IMF・Eurostat(コソボ)行が除外 |
| 作成機関 | — | 値を誰が編集したか(`COMPILING_ORG`)が行ごとに違い、機関ごとに規約が違う |
| 範囲 | — | API が500エラーの他フローや、SDG データベースなどは含まれない |
| 時点 | — | API が上書き型で版を持たない。取得日が版 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/undata-sdmx のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/undata-sdmx?blobs=true`）と Parquet フッターの取得（2026-10-24）
