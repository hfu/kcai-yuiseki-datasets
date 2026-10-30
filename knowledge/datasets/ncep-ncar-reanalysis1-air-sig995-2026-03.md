---
id: ncep-ncar-reanalysis1-air-sig995-2026-03
title: ncep-ncar-reanalysis1-air-sig995-2026-03 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ncep-ncar-reanalysis1-air-sig995-2026-03 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
  - Hugging Face API と Parquet のフッター（コミット ffabc47、2026-10-30）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-30
related:
  - ncep-cpc-global-ir-4km-2026-10
  - agera5-japan-monthly-temperature-1979-2026
dataset: yuiseki/ncep-ncar-reanalysis1-air-sig995-2026-03
verified_how: read-data
pattern: questions
finding:
  - NCEP/NCAR 再解析1の地表付近（シグマ0.995面）の気温の NetCDF（年ごと79ファイル、1948年〜2026-03-17）を、配布されたままで凍結したもの（約1.7GB）
---

## 要点

- NCEP/NCAR 再解析1の地表付近（シグマ0.995面）の気温の NetCDF（年ごと79ファイル、1948年〜2026-03-17）を、配布されたままで凍結したもの（約1.7GB）。`index.tsv`・`index.json`・提供元のページの保存を追加。Parquet は無い。
- 分類: 気象・地球物理の原本。元の情報源: NOAA PSL の NCEP/NCAR 再解析1「シグマ0.995面の気温」（1日4回、2.5°格子）。
- 権利: Hugging Face のタグは other。ファイルにライセンス文は無く、PSL が謝辞（data provided by the NOAA PSL…）を求める。「CC BY 風」とみなすのは管理者の読み。

## 規模と形（2026-10-30 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット ffabc47（最終更新 2026-10-30、2026-10-30 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 1.74 GB、ファイル 89 本 |
| Parquet | なし（元の配布物または JSONL のみ） |

## 答えうる問い

- 地表付近の気温の長期（1948年〜）の大規模な傾向
- 再解析の気温と、観測・AgERA5 との比較

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 原本性 | NetCDF は配布されたまま。提供元のページと一覧の保存、チェックサムを同梱 | — |
| Parquet 無し | — | NetCDF を自分で開く必要がある |
| 粗さ | — | 2.5°格子で、日本の地域の議論には粗い |
| 版 | — | ファイルに版の番号が無い。最新の更新日（2026-03-19）が名前の2026-03。2026年のファイルは部分的（3月17日まで）で、他は2023年以前の日付 |
| 権利 | — | ファイルにライセンス文は無く、謝辞の依頼のみ。CC BY 風とみなすのは管理者の読み |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/ncep-ncar-reanalysis1-air-sig995-2026-03 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
- Hugging Face API（`/api/datasets/yuiseki/ncep-ncar-reanalysis1-air-sig995-2026-03?blobs=true`）と Parquet フッターの取得（2026-10-30）
