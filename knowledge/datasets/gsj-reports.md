---
id: gsj-reports
title: gsj-reports で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/gsj-reports のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット d3128d8、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - nilim-disaster-reports
  - mlit-river-basin-overviews
  - moni1000-reports
  - rinya-forest-inventory
dataset: yuiseki/gsj-reports
verified_how: read-data
pattern: questions
finding:
  - 2誌のPDFの文字層を1ページ1行のJSONLにした49,065ページ、約2.6億字
---

## 要点

- 2誌のPDFの文字層を1ページ1行のJSONLにした49,065ページ、約2.6億字。Parquet 無し(JSONL 2本、386MB)。
- 分類: 知識・テキスト。元の情報源: 産総研 地質調査総合センター(GSJ)。
- 権利: CC BY 4.0(またはカード参照。権利の扱いは各カードの Rights/Licence)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d3128d8（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 386.1 MB、ファイル 7 本 |
| Parquet | なし（元の配布物または JSONL のみ） |

## 答えうる問い

- 日本の公的文書の全文検索・要約

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | JSONL は UTF-8。日本語が読める | — |
| 品質 | — | 古い号はOCR層の誤認識を含む(`について` が `にっいて` など)。U+FFFD が無い・`has_text` が真でも正しいとは限らない |
| レイアウト | — | `-layout` で、2段組の左右が1行に並ぶ。ヘッダー・ページ番号・キャプションが混ざる |
| 権利 | — | 公式製品ではなく、GSJの承認は無い。PDF・図は含まれない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/gsj-reports のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/gsj-reports?blobs=true`）と Parquet フッターの取得（2026-10-24）
