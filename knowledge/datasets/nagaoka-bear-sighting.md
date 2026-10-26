---
id: nagaoka-bear-sighting
title: nagaoka-bear-sighting で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/nagaoka-bear-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット 724bde2、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - kyoto-bear-sighting
  - gifu-bear-sighting
dataset: yuiseki/nagaoka-bear-sighting
verified_how: read-data
pattern: questions
finding:
  - 新潟県長岡市のクマの目撃・痕跡166件（平成26・27年度、2014-04-09〜2016-03-30）
---

## 要点

- 新潟県長岡市のクマの目撃・痕跡166件（平成26・27年度、2014-04-09〜2016-03-30）。
- 分類: クマ出没記録。元の情報源: 長岡市「クマ出没情報」（長岡市オープンデータ、危機管理防災本部）。
- 権利: CC BY（長岡市オープンデータ利用規約: CC BY 4.0）。改変の表示が必要。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 724bde2（最終更新 2026-10-26、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 0.2 MB、ファイル 14 本 |
| Parquet | 1 本、合計 0.0 MB、最大 0.0 MB |
| 行数 | 166（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/sighting.parquet`） | 12（うち文字列 6） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: sighting.parquet。他のファイルは未検査） |

## 答えうる問い

- 長岡市（栃尾・長岡・越路・山古志など）のクマの目撃・痕跡の分布（2014〜2015年度）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | UTF-8とShift_JISの両方が元にあり、同じ行であることを確認して UTF-8 から作成（カード） | — |
| 検証 | CSV と全行・全列を照合したとカードが述べる | — |
| 時点 | — | 2年度分のみ、2016年公表。ページの更新日（2026年4月1日）は更新を意味しない |
| 表記 | — | `kind` に `◆目撃` 17、末尾に空白のある `目撃 ` 1。日付の文言（目撃・痕跡）が `classification` と1行で違う（両方保持） |
| 番号 | — | `No` は年度ごとに振り直され、鍵にならない |
| 権利 | — | 改変した旨の表示が、市の規約で求められる |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/nagaoka-bear-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/nagaoka-bear-sighting?blobs=true`）と Parquet フッターの取得（2026-10-26）
