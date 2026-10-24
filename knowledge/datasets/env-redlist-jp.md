---
id: env-redlist-jp
title: env-redlist-jp で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/env-redlist-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 02f964f、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related: []
dataset: yuiseki/env-redlist-jp
verified_how: read-data
pattern: questions
finding:
  - 環境省の第5次レッドリスト(分類群ごとの CSV 原本と Parquet 8本)
---

## 要点

- 環境省の第5次レッドリスト(分類群ごとの CSV 原本と Parquet 8本)。絶滅危惧のカテゴリ(EX〜LP)が種ごとに付く。
- 分類: 日本の統計・公的GIS。元の情報源: 環境省 第5次レッドリスト。
- 権利: CC BY 4.0(環境省のクレジット)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 02f964f（最終更新 2026-10-05、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 0.8 MB、ファイル 21 本 |
| Parquet | 8 本、合計 0.3 MB、最大 0.1 MB |
| 行数 | 3,262（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/5th/birds.parquet`） | 178（うち文字列 38） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: birds.parquet、fungi.parquet。他のファイルは未検査） |

## 答えうる問い

- 分類群ごとのカテゴリ別の種数
- 2025年版と2026年版の更新差

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | Parquet は CSV の全値と一致するとカードが検証。正規化はしていない | — |
| 表記 | — | カテゴリの書き方が2025年ファイル(`絶滅危惧ⅠＡ類（CR）`)と2026年ファイル(`絶滅危惧IA類`)で違う。比較にはそろえる処理が要る |
| 列 | — | 分類群ごとに列構成が違う(2025年は植物・菌類など、2026年は鳥類など) |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/env-redlist-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/env-redlist-jp?blobs=true`）と Parquet フッターの取得（2026-10-24）
