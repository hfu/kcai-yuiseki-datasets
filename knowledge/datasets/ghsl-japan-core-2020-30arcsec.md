---
id: ghsl-japan-core-2020-30arcsec
title: ghsl-japan-core-2020-30arcsec で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ghsl-japan-core-2020-30arcsec のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 4ee7674、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - kontur-population-2023-11-01-22km
  - worldpop-jp-2026-01
  - worldpop-kor-population-2015-2030-1km-r2025a
dataset: yuiseki/ghsl-japan-core-2020-30arcsec
verified_how: read-data
pattern: questions
finding:
  - 2020年の居住人口（GHS-POP）と建物表面積（GHS-BUILT-S）を、各720万セルの多角形にした GeoParquet（5タイル×2種、合計1,440万行）
---

## 要点

- 2020年の居住人口（GHS-POP）と建物表面積（GHS-BUILT-S）を、各720万セルの多角形にした GeoParquet（5タイル×2種、合計1,440万行）。元の JRC の zip も併置。
- 分類: 人口・建物・土地被覆。元の情報源: 欧州委員会 JRC の GHSL R2023A E2020（GHS-POP、GHS-BUILT-S）、30秒、日本と周辺。
- 権利: CC BY 4.0（出典と製品の引用が必要）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 4ee7674（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 177.7 MB、ファイル 34 本 |
| Parquet | 10 本、合計 154.0 MB、最大 16.5 MB |
| 行数 | 14,400,000（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/parquet/population/R6_C32.parquet`） | 5（うち文字列 1） |
| 行グループ数（標本の最大） | 15 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: R6_C32.parquet。他のファイルは未検査） |

## 答えうる問い

- 日本とその周辺の人口分布・建物の分布（30秒格子、2020年）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 完全性 | ゼロの値も含む全セルを保持（NoData なし）。元の値と同じと検証（カード） | — |
| 分割 | タイル別（R5_C32…）のファイルで、必要な範囲だけ取れる | — |
| 意味 | — | GHS-POP は国勢調査などの合計をモデルで配分した推定で、セル単位の国勢調査の値ではない。GHS-BUILT-S もモデルの推定（m²） |
| 格子 | — | 30秒の角度格子で等積でない |
| 型 | — | タイルごとに地理変換・範囲・値の要約が違う（`profile.json`） |
| 範囲読み(実測) | — | タイル R6_C32 の bbox 読み（169セル）で 16.07MB／全体16.3MB（全量） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/ghsl-japan-core-2020-30arcsec のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/ghsl-japan-core-2020-30arcsec?blobs=true`）と Parquet フッターの取得（2026-10-26）
