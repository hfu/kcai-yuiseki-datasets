---
id: mlit-river-basin-overviews
title: mlit-river-basin-overviews で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/mlit-river-basin-overviews のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット bdd94d9、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - gsj-reports
  - nilim-disaster-reports
  - moni1000-reports
  - rinya-forest-inventory
dataset: yuiseki/mlit-river-basin-overviews
verified_how: read-data
pattern: questions
finding:
  - 一級水系の流域の地形・地質・気候・土地利用・歴史・災害を述べた115文書、9,894ページ、約610万字のJSONL
---

## 要点

- 一級水系の流域の地形・地質・気候・土地利用・歴史・災害を述べた115文書、9,894ページ、約610万字のJSONL。
- 分類: 知識・テキスト。元の情報源: 国土交通省。
- 権利: CC BY 4.0(またはカード参照。権利の扱いは各カードの Rights/Licence)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット bdd94d9（最終更新 2026-10-07、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 37.8 MB、ファイル 4 本 |
| Parquet | なし（元の配布物または JSONL のみ） |

## 答えうる問い

- 日本の公的文書の全文検索・要約

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | JSONL は UTF-8。日本語が読める | — |
| 権利 | — | 地方整備局や都道府県が作った資料では作成主体の規約が別に当たる可能性があり、個別確認はされていない |
| 内容 | — | 地名が密に出る。図表が多く、本文だけでは意味が取れないページがある |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/mlit-river-basin-overviews のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/mlit-river-basin-overviews?blobs=true`）と Parquet フッターの取得（2026-10-24）
