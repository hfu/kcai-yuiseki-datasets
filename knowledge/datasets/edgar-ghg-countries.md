---
id: edgar-ghg-countries
title: edgar-ghg-countries で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/edgar-ghg-countries のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 46b7502、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - undata-sdmx
  - faostat
dataset: yuiseki/edgar-ghg-countries
verified_how: read-data
pattern: questions
finding:
  - 国別・IPCCセクター別の年次・月次排出量(1970〜2025年、F-gases は1990〜)を、JRC の xlsx の zip のまま8本保持
---

## 要点

- 国別・IPCCセクター別の年次・月次排出量(1970〜2025年、F-gases は1990〜)を、JRC の xlsx の zip のまま8本保持。
- 分類: 世界の統計。元の情報源: EC-JRC EDGAR_2026_GHG の国別表。
- 権利: CC BY 4.0(CH4・N2O・F-gases・生物起源CO2のみ)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 46b7502（最終更新 2026-10-10、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 190.8 MB、ファイル 14 本 |
| Parquet | なし（元の配布物または JSONL のみ） |

## 答えうる問い

- 国別・部門別の温室効果ガス排出

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 原本性 | JRC が配る zip そのまま | — |
| 権利除外 | — | 化石CO2(IEA-EDGAR CO2)は CC BY-NC-ND 4.0 で含まれない。化石CO2を含む合計(AR5 GHG)も無い |
| 範囲 | — | 格子データは別データセット(edgar-ghg-grids) |
| 形式 | — | xlsx。Parquet 無し |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- xlsx の中のシート構成は未確認

## 出典

- yuiseki/edgar-ghg-countries のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/edgar-ghg-countries?blobs=true`）と Parquet フッターの取得（2026-10-24）
