---
id: un-wpp
title: un-wpp で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/un-wpp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット c403d78、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - worldbank-wdi
  - unhcr-refugee-stats
dataset: yuiseki/un-wpp
verified_how: read-data
pattern: questions
finding:
  - 1950年からの推計と2100年までの推計(年齢・性別、出生、死亡、生命表、純移動)
---

## 要点

- 1950年からの推計と2100年までの推計(年齢・性別、出生、死亡、生命表、純移動)。1998〜2024の全改訂版の CSV を原本で保持し、現行 WPP2024 を Parquet 53表(約2億行)で提供。
- 分類: 世界の統計。元の情報源: 国連 World Population Prospects(WPP、人口部)。
- 権利: CC BY 3.0 IGO。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット c403d78（最終更新 2026-10-10、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 11.70 GB、ファイル 127 本 |
| Parquet | 54 本、合計 3.19 GB、最大 220.8 MB |
| 行数 | 200,840,676（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/wpp2024/life_table_complete_medium_male_2024_2100.parquet`） | 29（うち文字列 9） |
| 行グループ数（標本の最大） | 250 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `Notes` 85.9%、`ISO3_code` 57.3%、`ISO2_code` 57.3% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 国別・年齢別の人口推計
- 中位・高位・低位の推計差

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 規模の扱い | Parquet は54本で表ごとに分かれ、必要な表だけ取れる。最大220.8MB | — |
| 量 | — | 全体11.7GB(原本の zip・gz が約8.5GB)。全部は落とさない |
| 集計行 | — | 国と地域・開発グループの集計が同じ表に混ざる |
| 更新 | — | 2026年に暫定更新(interim update)があり、版の扱いに注意(カード参照) |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 暫定更新の中身はカード参照。ここでは未検証

## 出典

- yuiseki/un-wpp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/un-wpp?blobs=true`）と Parquet フッターの取得（2026-10-24）
