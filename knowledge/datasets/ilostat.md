---
id: ilostat
title: ilostat で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ilostat のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 6f6d8ac、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - faostat
  - worldbank-wdi
dataset: yuiseki/ilostat
verified_how: read-data
pattern: questions
finding:
  - 1,963指標ファイル(.csv.gz)、約3.99億レコード、目次(英仏西)と辞書244ファイル
---

## 要点

- 1,963指標ファイル(.csv.gz)、約3.99億レコード、目次(英仏西)と辞書244ファイル。ミラーで、再変換していない。Parquet は無い。
- 分類: 世界の統計。元の情報源: ILO ILOSTAT 一括ダウンロード(2026-10-04取得)。
- 権利: CC BY 4.0(2023-05-03以降に公表された分のみ)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 6f6d8ac（最終更新 2026-10-10、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 2.66 GB、ファイル 2219 本 |
| Parquet | なし（元の配布物または JSONL のみ） |

## 答えうる問い

- 国別の労働力、雇用、賃金などの指標(元の分類で)

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 原本性 | ILO が配るファイルそのまま。行数は一覧の `n.records` と照合してある | — |
| 権利除外 | — | 公表日が2023-05-03より前の指標ファイルは CC BY の対象と言えないため除外(MANIFEST に列挙) |
| Parquet 無し | — | gz CSV を自分で開く。合計2.6GB |
| 更新 | — | サーバーが毎日再生成し旧版を残さない。この写しは1回分 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 指標ファイルの列構成の共通性は未確認

## 出典

- yuiseki/ilostat のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ilostat?blobs=true`）と Parquet フッターの取得（2026-10-24）
