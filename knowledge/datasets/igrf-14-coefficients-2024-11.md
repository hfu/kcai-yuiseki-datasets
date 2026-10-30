---
id: igrf-14-coefficients-2024-11
title: igrf-14-coefficients-2024-11 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/igrf-14-coefficients-2024-11 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
  - Hugging Face API と Parquet のフッター（コミット 011ed3b、2026-10-30）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-30
related:
  - ncep-ncar-reanalysis1-air-sig995-2026-03
dataset: yuiseki/igrf-14-coefficients-2024-11
verified_how: read-data
pattern: questions
finding:
  - IGRF-14 のシュミット準正規化球面調和係数（次数1〜13、1900〜2025年の26時点と、2025〜30年の永年変化）
---

## 要点

- IGRF-14 のシュミット準正規化球面調和係数（次数1〜13、1900〜2025年の26時点と、2025〜30年の永年変化）。元のファイルを無改変で置き、1係数1時点1行の縦持ち Parquet（5,265行）を併置。
- 分類: 気象・地球物理の原本。元の情報源: IAGA の国際標準地球磁場 IGRF-14 の球面調和係数（NOAA NCEI 配布、2024-11-18のファイル）。
- 権利: Hugging Face のタグは other（NCEI の製品ページの条件を引用）。製作者は IAGA ワーキンググループ V-MOD。

## 規模と形（2026-10-30 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 011ed3b（最終更新 2026-10-29、2026-10-30 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 0.1 MB、ファイル 10 本 |
| Parquet | 1 本、合計 0.0 MB、最大 0.0 MB |
| 行数 | 5,265（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/coefficients.parquet`） | 8（うち文字列 4） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: coefficients.parquet。他のファイルは未検査） |

## 答えうる問い

- ある地点・年の地磁気の主磁場を、利用者の選ぶパッケージで計算するための係数

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | 元のテキストを DuckDB で独立に縦持ちにして全セルを比較（差0）。ppigrf 2.1.0 での主磁場の計算と比べ、6地点・7時点で最大差0.00035 nT（検証用のコード。データではない） | — |
| キー | `kind`（g/h）・`n`・`m`・`epoch_label`・`epoch_year`・`series`（IGRF／DGRF／SV）で1行が決まる | — |
| 意味 | — | モデルの係数であって、磁場の値ではない。値は別のパッケージで計算する |
| 系列 | — | 1900〜1940年は IGRF、1945〜2020年は DGRF（確定）、2025年は IGRF（暫定）。IGRF の列は後の世代で置き換わる |
| 版 | — | IAGA が訂正や次の世代を出したら、このリポジトリは最新のファイルに追随する（現在の状態を置く型） |
| 永年変化 | — | `epoch_year` は永年変化（2025-30）の行でnull |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/igrf-14-coefficients-2024-11 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
- Hugging Face API（`/api/datasets/yuiseki/igrf-14-coefficients-2024-11?blobs=true`）と Parquet フッターの取得（2026-10-30）
