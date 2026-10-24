---
id: meta-range-maps-2022-05
title: meta-range-maps-2022-05 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/meta-range-maps-2022-05 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット c3450b4、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - meta-move-dist
dataset: yuiseki/meta-range-maps-2022-05
verified_how: read-data
pattern: questions
finding:
  - COVID-19 期の移動量の変化(2020年2月比)と1つの小域に留まった割合
---

## 要点

- COVID-19 期の移動量の変化(2020年2月比)と1つの小域に留まった割合。153か国19,142地域。
- 分類: 世界の地理。元の情報源: Meta Movement Range Maps(2020-03-01〜2022-05-22、終了済み)。
- 権利: CC BY 4.0(Meta と HDX のクレジット)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット c3450b4（最終更新 2026-10-02、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 218.7 MB、ファイル 11 本 |
| Parquet | 3 本、合計 89.1 MB、最大 38.7 MB |
| 行数 | 12,179,540（全 Parquet のフッターの合計） |
| 列数（代表ファイル `movement-range-maps/movement_range_2020.parquet`） | 10（うち文字列 7） |
| 行グループ数（標本の最大） | 53 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- パンデミック期の移動の変化

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 規模 | Parquet 3本(合計89MB) | — |
| 名前 | — | `NA` という名前の地域が898ある(台東区を含む)。名前でなく `polygon_id` で結合する |
| 終了 | — | データは2022-05-22で終わり、更新されない |
| サイズ | — | HDX の API が示す zip サイズが実体と食い違う(実体が正しい zip) |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/meta-range-maps-2022-05 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/meta-range-maps-2022-05?blobs=true`）と Parquet フッターの取得（2026-10-24）
