---
id: nilim-disaster-reports
title: nilim-disaster-reports で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/nilim-disaster-reports のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット c615f04、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - gsj-reports
  - mlit-river-basin-overviews
  - moni1000-reports
  - rinya-forest-inventory
dataset: yuiseki/nilim-disaster-reports
verified_how: read-data
pattern: questions
finding:
  - 国総研が単独で出し他の権利表記が無い26報告(883ページ)の本文JSONL
---

## 要点

- 国総研が単独で出し他の権利表記が無い26報告(883ページ)の本文JSONL。共同刊行・共著・判断不能の118報告は除外し、理由を記録。
- 分類: 知識・テキスト。元の情報源: 国土交通省 国土技術政策総合研究所(国総研)。
- 権利: CC BY 4.0(またはカード参照。権利の扱いは各カードの Rights/Licence)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット c615f04（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 4.5 MB、ファイル 9 本 |
| Parquet | なし（元の配布物または JSONL のみ） |

## 答えうる問い

- 日本の公的文書の全文検索・要約

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | JSONL は UTF-8。日本語が読める | — |
| 権利除外 | — | 共同刊行・共著などの118報告は含まれない(EXCLUDE.txt、RIGHTS_REVIEW.tsv) |
| 品質 | — | 5ページは空。2段組が1行に並ぶ。`report_title` に索引のリンク文字が混ざり、`event` は65PDF中52が「要調査」 |
| 内容 | — | 表紙・目次・奥付も含む |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/nilim-disaster-reports のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/nilim-disaster-reports?blobs=true`）と Parquet フッターの取得（2026-10-24）
