---
id: faostat
title: faostat で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/faostat のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 1908be2、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - ilostat
  - worldbank-wdi
dataset: yuiseki/faostat
verified_how: read-data
pattern: questions
finding:
  - 66のドメイン zip(Normalized の長持ち CSV と、地域・品目・要素・フラグの辞書)
---

## 要点

- 66のドメイン zip(Normalized の長持ち CSV と、地域・品目・要素・フラグの辞書)。ミラーで、Parquet は無い。
- 分類: 世界の統計。元の情報源: FAO FAOSTAT 一括ダウンロード(2026-10-04取得)。
- 権利: CC BY 4.0(2019-11-30以降。前の廃止系列3つは除外)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 1908be2（最終更新 2026-10-10、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 1.52 GB、ファイル 72 本 |
| Parquet | なし（元の配布物または JSONL のみ） |

## 答えうる問い

- 国別の生産・貿易・食料収支・土地利用・排出などの長期系列

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 原本性 | FAO の zip そのまま | — |
| 権利除外 | — | カタログ更新日が2019-11-30より前の3系列(食料援助、世帯調査指標、旧生産者価格)は含まれない |
| Parquet 無し | — | zip の中の CSV を自分で開く。1.5GB |
| 上書き | — | FAO が同名で上書きする。取得日が版 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/faostat のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/faostat?blobs=true`）と Parquet フッターの取得（2026-10-24）
