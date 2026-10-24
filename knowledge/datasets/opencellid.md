---
id: opencellid
title: opencellid で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/opencellid のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 82e4acd、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - geonames
  - worldpop-jp-2026-01
dataset: yuiseki/opencellid
verified_how: read-data
pattern: questions
finding:
  - 携帯基地局のセル1つ=1行(識別子と推定位置)
---

## 要点

- 携帯基地局のセル1つ=1行(識別子と推定位置)。550万行。元 csv.gz と GeoParquet(点)。
- 分類: 世界の地理。元の情報源: OpenCelliD の全世界エクスポート(日付スナップショット、2026-10-06)。
- 権利: CC BY-SA 4.0。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 82e4acd（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-sa-4.0 |
| 全体 | 246.0 MB、ファイル 7 本 |
| Parquet | 1 本、合計 126.5 MB、最大 126.5 MB |
| 行数 | 5,502,843（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/2026-10-06/cell_towers.parquet`） | 15（うち文字列 2） |
| 行グループ数（標本の最大） | 45 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 国・事業者別のセル密度
- LTE・NR の普及の地理

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | 点の GeoParquet(確認した1本には `geo` メタデータあり) | — |
| 精度 | — | 位置は寄稿者の測定からの推定で、アンテナの位置ではない。`range` が1000の行が57%、サンプル1件の行が916,581 |
| 偏り | — | 国ごとの件数は事業者網より寄稿者の偏りを映す |
| 継承 | — | CC BY-SA 4.0 のため派生物にも同じ条件が及ぶ |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/opencellid のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/opencellid?blobs=true`）と Parquet フッターの取得（2026-10-24）
