---
id: ksj-l01-land-price
title: ksj-l01-land-price で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ksj-l01-land-price のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 7e32fd1、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - ksj-p11-bus-stop-jp
  - estat-census-mesh-2020
dataset: yuiseki/ksj-l01-land-price
verified_how: read-data
pattern: questions
finding:
  - 地価公示の標準地(1点=1区画)の価格・住所・面積・用途・都市計画などの約100属性
---

## 要点

- 地価公示の標準地(1点=1区画)の価格・住所・面積・用途・都市計画などの約100属性。2019〜2026年の207,087区画年。全国と47県ごとの zip(384本)と、年ごとの Parquet 8本。
- 分類: 日本の統計・公的GIS。元の情報源: 国土交通省 国土数値情報 L01 地価公示(2019〜2026年)。
- 権利: 国土数値情報の利用規約(CC BY 4.0 互換)。出典表示が要る。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 7e32fd1（最終更新 2026-10-16、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 385.6 MB、ファイル 407 本 |
| Parquet | 8 本、合計 48.3 MB、最大 6.4 MB |
| 行数 | 207,087（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/2026.parquet`） | 157（うち文字列 54） |
| 行グループ数（標本の最大） | 47 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 標準地の価格を年・用途・地域で比べる
- 地価と周辺の施設・バス停・人口との関係を見る

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 元との対応 | zip を併置。取得日と Last-Modified が MANIFEST に残る | — |
| 訂正 | — | 元サイトは訂正のたびに同じファイルを上書きする(東京の住所の訂正など)。この写しは1回分 |
| 幾何 | — | Parquet 8本のうち確認した1本に `geo` メタデータが無かった(点の列の有無は未確認) |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 年をまたぐ標準地の同一性(標準地番号の継続性)

## 出典

- yuiseki/ksj-l01-land-price のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ksj-l01-land-price?blobs=true`）と Parquet フッターの取得（2026-10-24）
