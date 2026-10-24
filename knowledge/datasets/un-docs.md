---
id: un-docs
title: un-docs で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/un-docs のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 6cd1cf0、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - egov-laws-jp
dataset: yuiseki/un-docs
verified_how: read-data
pattern: questions
finding:
  - 39,363文書の本文
---

## 要点

- 39,363文書の本文。37,499件はテキスト層、1,864件はスキャンを tesseract で読んだもの。Parquet 1本(409MB、20行グループ)。
- 分類: 知識・テキスト。元の情報源: 国連総会・安保理の英語文書(1945〜2023)。
- 権利: other(国連文書。カード参照)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 6cd1cf0（最終更新 2026-09-21、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 409.4 MB、ファイル 5 本 |
| Parquet | 1 本、合計 409.4 MB、最大 409.4 MB |
| 行数 | 39,363（全 Parquet のフッターの合計） |
| 列数（代表ファイル `documents.parquet`） | 15（うち文字列 14） |
| 行グループ数（標本の最大） | 20 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `date_adopted_rule` 79.1%、`date_adopted` 79.1%、`date_adopted_raw` 79.1%、`date_other_rule` 53.7% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | `body` U+FFFD 2行・二重エンコード疑い 0行 |

## 答えうる問い

- 国連決議・文書の全文検索
- 年代別の語彙の変化

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 規模 | 1本だが行グループが20に分かれ、範囲でも読める | — |
| 品質 | — | スキャン由来の文書は OCR 誤りを含む。本文に U+FFFD を含む行がある(実測: 先頭3,000行中2) |
| 範囲 | — | 英語のみ。`pdf` 列が指す PDF の大半はリポジトリに無い |
| 位置 | — | 位置の列は無い |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/un-docs のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/un-docs?blobs=true`）と Parquet フッターの取得（2026-10-24）
