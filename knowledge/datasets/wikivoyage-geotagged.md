---
id: wikivoyage-geotagged
title: wikivoyage-geotagged で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/wikivoyage-geotagged のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 5b467da、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - wikipedia-geotagged
dataset: yuiseki/wikivoyage-geotagged
verified_how: read-data
pattern: questions
finding:
  - 座標つきの英語版 Wikivoyage 記事29,505件(2.34億字)
---

## 要点

- 座標つきの英語版 Wikivoyage 記事29,505件(2.34億字)。Parquet 1本。
- 分類: 知識・テキスト。元の情報源: Wikivoyage 20260901(英語)の geo_tags。
- 権利: CC BY-SA 4.0。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 5b467da（最終更新 2026-09-24、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-sa-4.0 |
| 全体 | 101.7 MB、ファイル 5 本 |
| Parquet | 1 本、合計 101.6 MB、最大 101.6 MB |
| 行数 | 29,505（全 Parquet のフッターの合計） |
| 列数（代表ファイル `20260901.en/train-00000-of-00001.parquet`） | 23（うち文字列 15） |
| 行グループ数（標本の最大） | 6 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `gt_region` 100.0%、`gt_name` 100.0%、`tags, list, element, type` 100.0%、`tags, list, element, name` 100.0% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（1 ファイル、全文字列列） | 20260901.en/train-00000-of-00001.parquet: `text` U+FFFD 2・二重エンコード疑い 1（29505行中） |

## 答えうる問い

- 旅行ガイドの記述から場所の説明を得る

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 規模 | Parquet 1本(102MB) | — |
| 場所でない記事 | — | 3.3%は Wikidata に項目が無い(旅程・トピック・フレーズブックなど) |
| 空の列 | — | 種類と国の列は全行空 |
| 継承 | — | CC BY-SA 4.0 |
| 文字(実測) | — | 全29,505行の `text` のうち U+FFFD が2行、二重エンコード疑いが1行 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/wikivoyage-geotagged のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/wikivoyage-geotagged?blobs=true`）と Parquet フッターの取得（2026-10-24）
