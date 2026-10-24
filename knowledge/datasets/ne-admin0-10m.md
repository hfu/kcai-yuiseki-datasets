---
id: ne-admin0-10m
title: ne-admin0-10m で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ne-admin0-10m のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット a891044、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - natural-earth
  - geonames
dataset: yuiseki/ne-admin0-10m
verified_how: read-data
pattern: questions
finding:
  - 国258、州・省4,596、米国の郡3,224の3層を、zip と型付き Parquet で凍結
---

## 要点

- 国258、州・省4,596、米国の郡3,224の3層を、zip と型付き Parquet で凍結。Wikidata ID つき。
- 分類: 世界の地理。元の情報源: Natural Earth 5.1.1(1:10m の admin0/admin1/admin2)。
- 権利: パブリックドメイン(Hugging Face のタグは other)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット a891044（最終更新 2026-09-26、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 46.7 MB、ファイル 16 本 |
| Parquet | 3 本、合計 25.0 MB、最大 16.8 MB |
| 行数 | 8,078（全 Parquet のフッターの合計） |
| 列数（代表ファイル `v5.1.1/parquet/ne_10m_admin_1_states_provinces.parquet`） | 126（うち文字列 36） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `FCLASS_ISO` 100.0%、`FCLASS_US` 100.0%、`FCLASS_AR` 100.0%、`FCLASS_VN` 100.0% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | `woe_label` U+FFFD 0行・二重エンコード疑い 91行；`woe_name` U+FFFD 0行・二重エンコード疑い 6行 |
| 全行の文字検査（2 ファイル、全文字列列） | v5.1.1/parquet/ne_10m_admin_1_states_provinces.parquet: `woe_label` U+FFFD 0・二重エンコード疑い 137（4596行中）、`woe_name` U+FFFD 0・二重エンコード疑い 6（4596行中）、`gns_name` U+FFFD 0・二重エンコード疑い 2（4596行中） |

## 答えうる問い

- 国・州の境界と Wikidata の結び付け

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| キー | `WIKIDATAID` は258か国すべてに入る(紛争地も) | — |
| 文字コード | — | admin1 の `woe_label` 4,596行中134行が二重エンコード(元の DBF の欠陥で、Parquet は忠実に保持)。例: `Paysandú` が `PaysandÃº` |
| 列名 | — | `WIKIDATAID`(国)と `wikidataid`(州)で大文字小文字が違う。正規化していない |
| 階層 | — | 第3階層は米国のみの郡 |
| 文字(実測) | — | 全4,596行の検査で、二重エンコード疑いは `woe_label` 137行・`woe_name` 6行・`gns_name` 2行（`Ã` を含むのは134行） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/ne-admin0-10m のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ne-admin0-10m?blobs=true`）と Parquet フッターの取得（2026-10-24）
