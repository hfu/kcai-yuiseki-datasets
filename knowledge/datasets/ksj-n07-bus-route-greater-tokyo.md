---
id: ksj-n07-bus-route-greater-tokyo
title: ksj-n07-bus-route-greater-tokyo で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ksj-n07-bus-route-greater-tokyo のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット f5dfc10、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - ksj-n07-bus-route-jp
  - ksj-p11-bus-stop-greater-tokyo
dataset: yuiseki/ksj-n07-bus-route-greater-tokyo
verified_how: read-data
pattern: questions
finding:
  - 埼玉・千葉・東京・神奈川(都道府県コード11〜14)のバス路線58,823本
---

## 要点

- 埼玉・千葉・東京・神奈川(都道府県コード11〜14)のバス路線58,823本。4県まとめて1本と県別。ksj-n07-bus-route-jp の部分集合。
- 分類: 日本の統計・公的GIS。元の情報源: 国土交通省 国土数値情報 N07 バスルート(2022年版 第2.0版)。
- 権利: 国土数値情報の利用規約(CC BY 4.0 互換)。2011年版は非商用で含まれない。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット f5dfc10（最終更新 2026-10-22、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 32.1 MB、ファイル 15 本 |
| Parquet | 5 本、合計 16.3 MB、最大 8.2 MB |
| 行数 | 117,646（全 Parquet のフッターの合計。全国1本と県別の本が同じ地物を二重に持つため、実際の件数はその約半分の 58,823。カードの件数と一致） |
| 列数（代表ファイル `parquet/bus_route.parquet`） | 5（うち文字列 5） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: bus_route.parquet、11.parquet。他のファイルは未検査） |

## 答えうる問い

- 事業者ごとの路線延長
- バス停(ksj-p11)と重ねて、路線網の密度を県ごとに比べる

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet。元の shp/dbf と件数・文字・頂点(1e-9度)まで一致するとカードが検証 | — |
| 文字コード | 日本語の事業者名が UTF-8 で読める | — |
| 粒度 | — | 「1本の線」は系統(ルート)ではない。神奈川中央交通だけで5,525本。系統数として数えない |
| 範囲 | — | 2022年8月ごろの資料。デマンドバス・高速バスは無い。路線名・時刻・頻度の属性は2011年版にしか無く、含まれない |
| 件数 | — | 全国版zipは353,453本で、県別zipの合計354,208本とは切り方が違う。Parquet は県別から作られている |
| 精度 | — | 位置は GSI 地図の15〜17ズームで目視確認した程度で、測量ではない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 重複する線15本(同一事業者・同一頂点)は残されている

## 出典

- yuiseki/ksj-n07-bus-route-greater-tokyo のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ksj-n07-bus-route-greater-tokyo?blobs=true`）と Parquet フッターの取得（2026-10-24）
