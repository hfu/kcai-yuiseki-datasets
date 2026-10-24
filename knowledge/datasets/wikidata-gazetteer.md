---
id: wikidata-gazetteer
title: wikidata-gazetteer で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/wikidata-gazetteer のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット ef7674b、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - geonames
  - wikipedia-geotagged
  - wikivoyage-geotagged
dataset: yuiseki/wikidata-gazetteer
verified_how: read-data
pattern: questions
finding:
  - 座標(P625)かWikipedia記事数(P1566)を持つ全項目12,205,328件と、552言語の名前62,506,107件、行政階層
---

## 要点

- 座標(P625)かWikipedia記事数(P1566)を持つ全項目12,205,328件と、552言語の名前62,506,107件、行政階層。Parquet 2本(最大508MB)。
- 分類: 知識・テキスト。元の情報源: Wikidata 20260831 ダンプ。
- 権利: CC0。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット ef7674b（最終更新 2026-09-21、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc0-1.0 |
| 全体 | 863.4 MB、ファイル 6 本 |
| Parquet | 2 本、合計 863.4 MB、最大 508.4 MB |
| 行数 | 74,711,435（全 Parquet のフッターの合計） |
| 列数（代表ファイル `names.parquet`） | 4（うち文字列 4） |
| 行グループ数（標本の最大） | 126 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 地名の多言語名寄せ
- Wikipedia の記事数で見た知名度

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| ライセンス | CC0 で最も制約が少ない | — |
| 場所でないもの | — | 座標を持つ項目を機械的に選ぶので、言語(729件。フランス語がパリの座標)、人物などが入る |
| 言語の偏り | — | 日本語名は場所の4.0%にしか無い。`ceb` が3,459,736ラベル(ボット生成) |
| 結合 | — | GeoNames ID を持つのは33.2%。GeoNames と独立した情報源でもある |
| 量 | — | 2本の行数の合計は74,711,435(場所12,205,328+名前62,506,107) |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/wikidata-gazetteer のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/wikidata-gazetteer?blobs=true`）と Parquet フッターの取得（2026-10-24）
