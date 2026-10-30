---
id: landsat5-fagus-crenata-sites-jp-2026-10
title: landsat5-fagus-crenata-sites-jp-2026-10 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/landsat5-fagus-crenata-sites-jp-2026-10 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
  - Hugging Face API と Parquet のフッター（コミット 939ee55、2026-10-30）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-30
related:
  - fagus-crenata-masting-jp-2026-06
  - akita-vegetation-2024
dataset: yuiseki/landsat5-fagus-crenata-sites-jp-2026-10
verified_how: read-data
pattern: questions
finding:
  - ブナの豊凶データの102地点（東北98・渡島4）の周辺300m以内について、1989〜2008年の4〜5月と7〜8月の全ての Landsat 5 の撮影から、地表反射率とQAを抽出した表
---

## 要点

- ブナの豊凶データの102地点（東北98・渡島4）の周辺300m以内について、1989〜2008年の4〜5月と7〜8月の全ての Landsat 5 の撮影から、地表反射率とQAを抽出した表。`site_acquisitions`（地点×撮影）、`pixels`（地点×撮影×画素）、`items`（STACアイテム）、`sites`。豊凶の結果は含まず、後で結ぶための観測表。
- 分類: ブナの豊凶。元の情報源: USGS Landsat 4-5 TM Collection 2 Level-2（Microsoft Planetary Computer の写し）を、ブナ豊凶の102地点の周辺300m以内で抽出。
- 権利: Hugging Face のタグは other（USGS の成果物はパブリックドメイン。地点は Dryad の CC0 から）。

## 規模と形（2026-10-30 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 939ee55（最終更新 2026-10-28、2026-10-30 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 44.9 MB、ファイル 9 本 |
| Parquet | 4 本、合計 44.9 MB、最大 44.2 MB |
| 行数 | 7,390,305（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/pixels.parquet`） | 9（うち文字列 1） |
| 行グループ数（標本の最大） | 8 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: pixels.parquet。他のファイルは未検査） |

## 答えうる問い

- ブナ豊凶の衛星による代理指標（NDVI・NDMI など）の組み立て
- 撮影日・雲・QAの条件で使える観測を絞る

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 再現性 | `PROCESSING.json`（定数・QAの規則・ソフトの版・件数・データのSHA-256）、`scripts/landsat.py` を同梱 | — |
| 分割 | 4つの表に分けてあり、必要な粒度（地点×撮影／画素）を選べる | — |
| 意味 | — | 300mの円は森林のマスクではなく、道路・伐採地・他の木が入る |
| 時期 | — | 撮影日は季節の窓の中で年・地点ごとに違い、フェノロジー（季節の進み）の違いが変動に混じる |
| 範囲 | — | Landsat 5 のみ。Landsat 7 を混ぜるにはセンサ間の調整が要る |
| 豊凶の結果 | — | 含まれない（別の fagus-crenata-masting-jp-2026-06 と結ぶ） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 画素表の大きさと QA 条件ごとの有効画素の割合は、カードの部分を読んだのみ

## 出典

- yuiseki/landsat5-fagus-crenata-sites-jp-2026-10 のデータセットカード（README、Hugging Face 上の main、2026-10-30 取得）
- Hugging Face API（`/api/datasets/yuiseki/landsat5-fagus-crenata-sites-jp-2026-10?blobs=true`）と Parquet フッターの取得（2026-10-30）
