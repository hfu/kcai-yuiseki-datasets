---
id: osm-wiki
title: osm-wiki で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/osm-wiki のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット ada3a2d、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-tag-corpus
  - text2geoql
dataset: yuiseki/osm-wiki
verified_how: read-data
pattern: questions
finding:
  - OSM Wiki 8言語78,178ページの平文
---

## 要点

- OSM Wiki 8言語78,178ページの平文。1ページ1行。Parquet 1本(159MB、79行グループ)。
- 分類: OSM とその派生。元の情報源: OSM Wiki の2026-01-30全履歴ダンプ(2026-09-17抽出)。
- 権利: CC BY-SA 2.0(Hugging Face のタグは無し。地図データの ODbL とは別)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット ada3a2d（最終更新 2026-09-17、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | （なし） |
| 全体 | 159.3 MB、ファイル 5 本 |
| Parquet | 1 本、合計 159.2 MB、最大 159.2 MB |
| 行数 | 78,178（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/train-00000-of-00001.parquet`） | 8（うち文字列 6） |
| 行グループ数（標本の最大） | 79 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | `text` U+FFFD 1行・二重エンコード疑い 2行 |

## 答えうる問い

- タグの説明の検索
- 言語間のページ対応

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 抽出 | wikitext をテンプレートごと解いて、タグの表のセルを残す(正規表現で消さない) | — |
| リダイレクト | — | リダイレクト32,656件を除外 |
| 短い・長いページ | — | 30字未満が814、30万字超が20(データの作業用ページ) |
| 時点 | — | ダンプは2026-01-30。wiki はその後進んでいる |
| 文字 | — | 1ページに U+FFFD を含む(実測: 先頭3,000行中1。元ページに由来するかは未確認) |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/osm-wiki のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/osm-wiki?blobs=true`）と Parquet フッターの取得（2026-10-24）
