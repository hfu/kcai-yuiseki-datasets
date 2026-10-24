---
id: osm-tokyo23-questions
title: osm-tokyo23-questions で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/osm-tokyo23-questions のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 75b757e、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-tokyo23-qa-2026-08
  - osm-tokyo23-src-2026-08
dataset: yuiseki/osm-tokyo23-questions
verified_how: read-data
pattern: questions
finding:
  - OSM から答えられるよう書かれた23区の英語の質問215問
---

## 要点

- OSM から答えられるよう書かれた23区の英語の質問215問。答えは付けない(答えは抽出した日に属するため)。
- 分類: OSM とその派生。元の情報源: 人が書いた23区の質問215問(20種類)。
- 権利: ODbL。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 75b757e（最終更新 2026-09-23、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 0.1 MB、ファイル 6 本 |
| Parquet | 1 本、合計 0.0 MB、最大 0.0 MB |
| 行数 | 215（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/train-00000-of-00001.parquet`） | 30（うち文字列 30） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `count` 99.5%、`neighbour_1` 99.5%、`neighbour_2` 99.5%、`name` 96.7% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: train-00000-of-00001.parquet。他のファイルは未検査） |

## 答えうる問い

- 地理質問応答システムの評価用の問い

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 設計 | 答えを持たないので、凍結版ごとに答えを計算し直せる | — |
| 範囲 | — | 英語の質問のみ |
| 依存 | — | 答えを得るには osm-tokyo23-src の同じスナップショットが要る |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/osm-tokyo23-questions のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/osm-tokyo23-questions?blobs=true`）と Parquet フッターの取得（2026-10-24）
