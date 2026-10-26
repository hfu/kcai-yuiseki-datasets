---
id: kamisunagawa-higuma-sighting
title: kamisunagawa-higuma-sighting で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/kamisunagawa-higuma-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 0a6f16b、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - akita-kumadas-wildlife-sighting
dataset: yuiseki/kamisunagawa-higuma-sighting
verified_how: read-data
pattern: questions
finding:
  - 北海道上砂川町のヒグマの出没105件（2024-05-11〜2026-08-19、R6〜R8）
---

## 要点

- 北海道上砂川町のヒグマの出没105件（2024-05-11〜2026-08-19、R6〜R8）。町の全記録。
- 分類: クマ出没記録。元の情報源: 上砂川町「ヒグマ出没マップ」（BODIK、令和6・7・8年度の3エントリー）。
- 権利: CC BY 4.0（`cc-by-40-intl`）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 0a6f16b（最終更新 2026-10-26、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 0.1 MB、ファイル 13 本 |
| Parquet | 1 本、合計 0.0 MB、最大 0.0 MB |
| 行数 | 105（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/sighting.parquet`） | 18（うち文字列 12） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `source_id` 91.4%、`address_text` 86.7%、`town` 86.7%、`lot` 86.7% |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: sighting.parquet。他のファイルは未検査） |

## 答えうる問い

- 北海道の小さな町のヒグマの出没の時期と場所

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | R6のCSVは Shift_JIS、他は UTF-8。Parquet は日本語を保持し、元の CSV を併置 | — |
| 検証 | 各 CSV と全行・全列を照合したとカードが述べる | — |
| 規模 | — | 105件と極めて小さい。R8は2026-09-14時点で未完 |
| 列 | — | 3つのCSVで列が違う（R6は住所を分割、R7・R8は1文）。1つの表に寄せて、無い列はnull。自治体コードは `14257` と `014257` の表記ゆれ（原本のまま） |
| 意味 | — | 町の報告（目撃・痕跡・糞）で、個体数調査ではない |
| 座標系 | — | 測地系は示されず、WGS 84 を仮定 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/kamisunagawa-higuma-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/kamisunagawa-higuma-sighting?blobs=true`）と Parquet フッターの取得（2026-10-26）
