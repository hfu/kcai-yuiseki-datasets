---
id: text2geoql
title: text2geoql で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/text2geoql のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 9f8b46b、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-tag-corpus
  - osm-tokyo23-qa-2026-08
dataset: yuiseki/text2geoql
verified_how: read-data
pattern: questions
finding:
  - 小型言語モデル向けの合成データ
---

## 要点

- 小型言語モデル向けの合成データ。約4,900件の検証済み対(Overpass API で1件以上返ることを確認)、148のPOI分類。
- 分類: OSM とその派生。元の情報源: TRIDENT 中間言語から Overpass QL への合成対。
- 権利: ODbL。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 9f8b46b（最終更新 2026-08-29、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 0.2 MB、ファイル 3 本 |
| Parquet | 1 本、合計 0.2 MB、最大 0.2 MB |
| 行数 | 4,897（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/train-00000-of-00001.parquet`） | 4（うち文字列 4） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 自然言語から Overpass QL への変換モデルの学習

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | クエリは公開 Overpass API で空でないことを確認済み(カード) | — |
| 評価 | — | 100.0%(112/112)という結果は「空でない」ことの厳密評価で、意味の正しさの評価ではない |
| 時点 | — | Overpass の応答は時点で変わる |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/text2geoql のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/text2geoql?blobs=true`）と Parquet フッターの取得（2026-10-24）
