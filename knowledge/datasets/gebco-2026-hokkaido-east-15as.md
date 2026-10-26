---
id: gebco-2026-hokkaido-east-15as
title: gebco-2026-hokkaido-east-15as で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/gebco-2026-hokkaido-east-15as のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 5da3260、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - ctrees-agb-hokkaido-east-100m
  - gsi-dem-fuji-z14-100m-2026-10-25
dataset: yuiseki/gebco-2026-hokkaido-east-15as
verified_how: read-data
pattern: questions
finding:
  - GEBCO 2026（海陸の15秒格子）の北海道東方の3°×3°を、画素ごとの長方形の多角形（518,400件、720×720）と標高（m、負は水深）にした GeoParquet
---

## 要点

- GEBCO 2026（海陸の15秒格子）の北海道東方の3°×3°を、画素ごとの長方形の多角形（518,400件、720×720）と標高（m、負は水深）にした GeoParquet。
- 分類: 北海道東部の窓抽出。元の情報源: GEBCO_2026 グリッド（CEDA アーカイブのタイル）の北海道東方の3°×3°。
- 権利: Hugging Face のタグは other（CEDA の OGL v3.0、GEBCO の条件）。出典の表示が必要。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 5da3260（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 3.9 MB、ファイル 4 本 |
| Parquet | 1 本、合計 3.9 MB、最大 3.9 MB |
| 行数 | 518,400（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/elevation.parquet`） | 2（うち文字列 0） |
| 行グループ数（標本の最大） | 17 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 文字の検査 | 文字列の列が無い（検査不要） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: elevation.parquet。他のファイルは未検査） |

## 答えうる問い

- 東部北海道沖の海底地形の標高・水深

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet 1.1.0、EPSG:4326。標高は符号つき16ビット整数の値そのまま | — |
| 意味 | — | 観測と推定が混ざった編集済みの地形モデル。15秒のセルが、元の測定の解像度や精度を意味しない。浅海では平均海面以外の鉛直基準の入力がありうる |
| 範囲 | — | TID（元データの種別）レイヤーを含まない。航行などの安全に関わる用途には使えない（カード） |
| 権利 | — | 公式の GEBCO・CEDA の製品ではなく、承認も受けていない |
| 範囲読み(実測) | — | terrio-js の bbox 読み（25画素）で 3.91MB／全体3.90MB（全量） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/gebco-2026-hokkaido-east-15as のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/gebco-2026-hokkaido-east-15as?blobs=true`）と Parquet フッターの取得（2026-10-26）
