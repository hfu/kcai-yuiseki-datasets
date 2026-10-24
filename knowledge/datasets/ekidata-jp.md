---
id: ekidata-jp
title: ekidata-jp で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ekidata-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット a333210、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - ksj-p11-bus-stop-jp
dataset: yuiseki/ekidata-jp
verified_how: read-data
pattern: questions
finding:
  - 鉄道事業者・路線・駅・隣接駅(join)・都道府県のマスター
---

## 要点

- 鉄道事業者・路線・駅・隣接駅(join)・都道府県のマスター。日付つきファイルごとに1サブセット、CSV と型付き Parquet(駅は点つき)。
- 分類: 日本の統計・公的GIS。元の情報源: 駅データ.jp(株式会社バリューアンドビジョン)の無料CSV。
- 権利: 駅データ.jp の利用規約(他。無償再配布は無改変のみ)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット a333210（最終更新 2026-10-05、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 14.4 MB、ファイル 51 本 |
| Parquet | 23 本、合計 4.1 MB、最大 0.6 MB |
| 行数 | 130,805（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/2026-10-05/station.2026-07-13.parquet`） | 16（うち文字列 8） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `station_name_r` 100.0%、`station_name_k` 100.0% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 駅の位置と路線の接続
- 駅の開業・廃止の追跡

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | 駅の GeoParquet 1.0.0。CRS 記録なし | — |
| 検証 | CSV と Parquet の全値が一致するとカードが検証 | — |
| 範囲 | — | 新幹線駅が無い(無料版の仕様)。有料項目の `station_name_k`、`station_name_r`、`line_type` は全行空 |
| 日付 | — | `open_ymd` が `0000-00-00` の駅が10,962中10,584 |
| 権利 | — | 再配布の条件が他と違い(無改変・無償)、派生物の再配布は別に確認が要る |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/ekidata-jp のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ekidata-jp?blobs=true`）と Parquet フッターの取得（2026-10-24）
