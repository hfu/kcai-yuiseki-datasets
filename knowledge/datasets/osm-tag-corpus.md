---
id: osm-tag-corpus
title: osm-tag-corpus で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/osm-tag-corpus のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 1e95497、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-wiki
  - text2geoql
dataset: yuiseki/osm-tag-corpus
verified_how: read-data
pattern: questions
finding:
  - OSM のタグ9,803種の多言語説明・関連語・世界での使用回数
---

## 要点

- OSM のタグ9,803種の多言語説明・関連語・世界での使用回数。埋め込み用の素材で、埋め込みも固定文も付けない。
- 分類: OSM とその派生。元の情報源: OSM Wiki のタグ記述と taginfo の使用回数。
- 権利: ODbL(wiki 由来の説明文の扱いはカード参照)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 1e95497（最終更新 2026-09-07、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 6.6 MB、ファイル 5 本 |
| Parquet | 1 本、合計 6.6 MB、最大 6.6 MB |
| 行数 | 31,913（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/train-00000-of-00001.parquet`） | 12（うち文字列 11） |
| 行グループ数（標本の最大） | 32 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `related_terms, list, element` 70.6% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: train-00000-of-00001.parquet。他のファイルは未検査） |

## 答えうる問い

- タグの意味検索の埋め込み実験

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 設計 | 文の組み立て方を呼び出し側に任せる | — |
| 範囲 | — | 埋め込みは無い。使用回数は取得時点の値 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/osm-tag-corpus のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/osm-tag-corpus?blobs=true`）と Parquet フッターの取得（2026-10-24）
