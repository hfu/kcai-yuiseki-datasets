---
id: pwt
title: pwt で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/pwt のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 77cf702、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - maddison-project
  - worldbank-wdi
dataset: yuiseki/pwt
verified_how: read-data
pattern: questions
finding:
  - PWT の7リリース
---

## 要点

- PWT の7リリース。リリースごとの主表と、国民経済計算など他の表を、`<release>.<table>` のサブセットで保持(41 Parquet)。Stata・xlsx・zip の原本も併置。
- 分類: 世界の統計。元の情報源: Penn World Table 8.0〜11.0(グローニンゲン大学 GGDC)。
- 権利: CC BY 4.0。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 77cf702（最終更新 2026-10-05、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 265.7 MB、ファイル 157 本 |
| Parquet | 41 本、合計 41.4 MB、最大 2.1 MB |
| 行数 | 1,552,050（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/11.0/esh_bilateral_cor.parquet`） | 4（うち文字列 2） |
| 行グループ数（標本の最大） | 4 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: esh_bilateral_cor.parquet、depreciation_rates.parquet。他のファイルは未検査） |

## 答えうる問い

- 国別の実質GDP・人口・雇用・資本・TFP の長期比較
- リリース間の改訂

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 原本の選び方 | Stata を正としている。xlsx は一部の表で有効桁が丸められている(8.1・9.0の国民経済計算は4桁) | — |
| 検証 | 各サブセットの全値が Stata と一致するとカードが検証 | — |
| 原本の不一致 | — | pwt81.xlsx は10,357行、pwt81.dta は10,354行で、ジンバブエ2009〜2011が通貨違いで重複して入っている。xlsx を正にしない |
| 結合 | — | リリースを積むと国コードや列の意味が変わる。リリースごとに読む |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/pwt のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/pwt?blobs=true`）と Parquet フッターの取得（2026-10-24）
