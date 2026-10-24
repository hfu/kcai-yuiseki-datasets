---
id: wikipedia-geotagged
title: wikipedia-geotagged で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/wikipedia-geotagged のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 24e53f6、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - wikidata-gazetteer
  - wikivoyage-geotagged
dataset: yuiseki/wikipedia-geotagged
verified_how: read-data
pattern: questions
finding:
  - 座標つき記事の本文
---

## 要点

- 座標つき記事の本文。英語1,374,056件(43億字)、日本語218,496件(4.35億字)。Parquet 7本。
- 分類: 知識・テキスト。元の情報源: Wikipedia 20260901 ダンプ(英語・日本語)の geo_tags。
- 権利: CC BY-SA 4.0。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 24e53f6（最終更新 2026-09-24、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-sa-4.0 |
| 全体 | 2.20 GB、ファイル 11 本 |
| Parquet | 7 本、合計 2.20 GB、最大 411.1 MB |
| 行数 | 1,592,552（全 Parquet のフッターの合計） |
| 列数（代表ファイル `20260901.en/train-00000-of-00005.parquet`） | 23（うち文字列 15） |
| 行グループ数（標本の最大） | 95 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `gt_name` 98.1%、`tags, list, element, name` 80.4%、`tags, list, element, region` 75.4%、`gt_region` 68.5% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 20260901.en/train-00004-of-00005.parquet: `text` U+FFFD 0・二重エンコード疑い 3（99056行中）；20260901.ja/train-00001-of-00002.parquet: `text` U+FFFD 0・二重エンコード疑い 1（33496行中） |

## 答えうる問い

- 場所についての記述の収集
- 座標付き記事と Wikidata の対応

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 選び方 | MediaWiki の GeoData(geo_tags)に基づくので、場所かどうかを推定でなく編集者の付与で決めている | — |
| 場所でない記事 | — | 英語記事の6.1%は場所でない(人物の出生地、本社の所在地など)。wikidata-gazetteer に qid が無い記事 |
| 継承 | — | CC BY-SA 4.0 |
| 範囲 | — | 英語と日本語のみ。リダイレクトと記事以外の名前空間は除外 |
| 文字(実測) | — | 検査した2ファイルの `text` に、二重エンコード疑いが英語3行（99,056行中）・日本語1行（33,496行中）。記事が文字化けの話をしている可能性もあり、確定していない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/wikipedia-geotagged のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/wikipedia-geotagged?blobs=true`）と Parquet フッターの取得（2026-10-24）
