---
id: ucdp-ged
title: ucdp-ged で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ucdp-ged のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット d72fe7e、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - unhcr-refugee-stats
dataset: yuiseki/ucdp-ged
verified_how: read-data
pattern: questions
finding:
  - 1989年以降の組織的暴力のイベント1件=1行(場所・日時・当事者・死者数)
---

## 要点

- 1989年以降の組織的暴力のイベント1件=1行(場所・日時・当事者・死者数)。版ごとのサブセットと型付き GeoParquet 8本。
- 分類: 世界の統計。元の情報源: Uppsala Conflict Data Program GED(版19.1〜26.1の8版)。
- 権利: CC BY 4.0(UCDPが挙げる文献の引用が条件)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d72fe7e（最終更新 2026-10-02、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 399.2 MB、ファイル 36 本 |
| Parquet | 8 本、合計 193.4 MB、最大 35.6 MB |
| 行数 | 2,403,936（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/26.1/ged.parquet`） | 50（うち文字列 21） |
| 行グループ数（標本の最大） | 9 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `gwnob` 90.4% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | parquet/26.1/ged.parquet: `source_article` U+FFFD 1・二重エンコード疑い 16（417968行中）、`source_headline` U+FFFD 1・二重エンコード疑い 15（417968行中）、`where_coordinates` U+FFFD 0・二重エンコード疑い 1（417968行中）、`where_description` U+FFFD 0・二重エンコード疑い 2（417968行中）；parquet/19.1/ged.parquet: `source_article` U+FFFD 0・二重エンコード疑い 1（152616行中）、`where_coordinates` U+FFFD 0・二重エンコード疑い 1（152616行中） |

## 答えうる問い

- 紛争イベントの時空間分布
- 当事者別の死者数の推移

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet 1.0.0、全行に点。座標フィルタと幾何フィルタが同じ事象を返すとカードが検証 | — |
| 出典列 | — | `source_*` は報道の出典・日付・見出しの引用で、26.1 では97,496行が空(多くは2013年以前)。見出しの権利は未確認とカードが述べる |
| 版 | — | 版ごとにイベントが追加・修正される。積み上げない |
| 引用条件 | — | UCDP が指定する文献を引用する条件つきの CC BY |
| 文字(実測) | — | 報道の引用列に、二重エンコードの疑いが少数ある(26.1: `source_article` 16行・`source_headline` 15行、41.8万行中)。U+FFFD も各1行。元の報道テキスト由来とみられるが、元を確認していない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/ucdp-ged のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ucdp-ged?blobs=true`）と Parquet フッターの取得（2026-10-24）
