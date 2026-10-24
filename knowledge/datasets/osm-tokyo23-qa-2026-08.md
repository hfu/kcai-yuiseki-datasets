---
id: osm-tokyo23-qa-2026-08
title: osm-tokyo23-qa-2026-08 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/osm-tokyo23-qa-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット d44f06a、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-tokyo23-questions
  - osm-tokyo23-src-2026-08
dataset: yuiseki/osm-tokyo23-qa-2026-08
verified_how: read-data
pattern: questions
finding:
  - 215問の答えと、それぞれを導いた SQL/Overpass QL
---

## 要点

- 215問の答えと、それぞれを導いた SQL/Overpass QL。聞き返し要否つき。
- 分類: OSM とその派生。元の情報源: osm-tokyo23-questions の215問の答え(凍結抽出から計算)。
- 権利: ODbL。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d44f06a（最終更新 2026-09-23、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 0.4 MB、ファイル 5 本 |
| Parquet | 1 本、合計 0.4 MB、最大 0.4 MB |
| 行数 | 215（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/train-00000-of-00001.parquet`） | 18（うち文字列 18） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `ask` 91.6%、`ambiguity` 88.8%、`interpretations` 83.7%、`on_the_edge` 79.1% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: train-00000-of-00001.parquet。他のファイルは未検査） |

## 答えうる問い

- 質問応答システムのスコア付け
- 曖昧さ・答えられなさの扱いの評価

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 答えの由来 | 答えは書いたのでなく、エンジンが返した値。クエリは AI(Claude Code)が書き、質問は人が書いた、とカードが明記 | — |
| 種類 | — | answer_kind は value 179、ambiguous 35(answer 11・ask 18・tie 6)、unanswerable 1。単一の正解がある問いは約83% |
| 版依存 | — | 答えは2026-08-31のスナップショットにのみ有効 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/osm-tokyo23-qa-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/osm-tokyo23-qa-2026-08?blobs=true`）と Parquet フッターの取得（2026-10-24）
