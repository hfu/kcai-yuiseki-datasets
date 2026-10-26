---
id: timezone-boundary-builder-2026d
title: timezone-boundary-builder-2026d で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/timezone-boundary-builder-2026d のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット cc26444、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - natural-earth
dataset: yuiseki/timezone-boundary-builder-2026d
verified_how: read-data
pattern: questions
finding:
  - タイムゾーンの境界の多角形（`tzid` つき）を3つの設定（全ゾーン、1970年以降同じ、現在同じ）の GeoParquet にしたもの
---

## 要点

- タイムゾーンの境界の多角形（`tzid` つき）を3つの設定（全ゾーン、1970年以降同じ、現在同じ）の GeoParquet にしたもの。元の GeoJSON zip と、統合した識別子の説明も併置。
- 分類: 地形・基盤。元の情報源: Timezone Boundary Builder 2026d（2026-09-16公開）。
- 権利: ODbL 1.0（share-alike）。「Contains information from Timezone Boundary Builder…」の表示が必要。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット cc26444（最終更新 2026-10-25、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | odbl |
| 全体 | 333.9 MB、ファイル 18 本 |
| Parquet | 3 本、合計 211.7 MB、最大 90.0 MB |
| 行数 | 785（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/timezones.parquet`） | 2（うち文字列 1） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: timezones.parquet。他のファイルは未検査） |

## 答えうる問い

- 座標からタイムゾーンを引く
- 統合した設定（1970年以降同じ・現在同じ）の違い

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| キー | `tzid` が特徴量の鍵。座標順は GeoJSON の経度・緯度 | — |
| 再現性 | リリースの zip と SHA-256 を同梱 | — |
| 設定 | — | `same-since-now` は現在の時刻が同じゾーンを統合しており、IANA 識別子の完全な一覧ではない |
| 継承 | — | ODbL の share-alike が派生物に及ぶ |
| 規模 | — | Parquet は3本で合計785特徴量だが、形が大きく合計212MB |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 海上のゾーンの扱いは未確認

## 出典

- yuiseki/timezone-boundary-builder-2026d のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/timezone-boundary-builder-2026d?blobs=true`）と Parquet フッターの取得（2026-10-26）
