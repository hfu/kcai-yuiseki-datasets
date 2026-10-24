---
id: scp-jp-plain
title: scp-jp-plain で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/scp-jp-plain のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 915aa2e、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related: []
dataset: yuiseki/scp-jp-plain
verified_how: read-data
pattern: questions
finding:
  - SCP財団日本語版の本文999件
---

## 要点

- SCP財団日本語版の本文999件。CC BY-SA 3.0(タグ)。
- 分類: 旧作(2024年)。元の情報源: (カードに記載なし)。
- 権利: Hugging Face のタグを参照。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 915aa2e（最終更新 2024-03-24、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-sa-3.0 |
| 全体 | 5.3 MB、ファイル 3 本 |
| Parquet | 1 本、合計 5.3 MB、最大 5.3 MB |
| 行数 | 999（全 Parquet のフッターの合計） |
| 列数（代表ファイル `data/train-00000-of-00001.parquet`） | 2（うち文字列 2） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: train-00000-of-00001.parquet。他のファイルは未検査） |

## 答えうる問い

- 日本語の言語モデルの学習データとして

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 規模 | Parquet 1本で小さい | — |
| 継承 | — | CC BY-SA 3.0(タグ)。元の著者表示が必要か未確認 |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 地理との関係は無い。2024年3〜4月の更新で、後のデータセット群と作りが違う(カードが定型)

## 出典

- yuiseki/scp-jp-plain のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/scp-jp-plain?blobs=true`）と Parquet フッターの取得（2026-10-24）
