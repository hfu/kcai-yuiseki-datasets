---
id: kyoto-bear-sighting
title: kyoto-bear-sighting で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/kyoto-bear-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット a2a50c4、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - gifu-bear-sighting
  - nagaoka-bear-sighting
dataset: yuiseki/kyoto-bear-sighting
verified_how: read-data
pattern: questions
finding:
  - ツキノワグマの目撃10,225件（2009-04-08〜2018-12-10）
---

## 要点

- ツキノワグマの目撃10,225件（2009-04-08〜2018-12-10）。場所・環境区分・成獣・幼獣・その他の頭数・状況・処置。
- 分類: クマ出没記録。元の情報源: 京都府「クマ目撃情報」（BODIK、情報政策課。FY2009〜FY2018の統合版）。
- 権利: CC BY 4.0（`cc-by-40-intl`）。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット a2a50c4（最終更新 2026-10-26、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 2.7 MB、ファイル 9 本 |
| Parquet | 1 本、合計 0.6 MB、最大 0.6 MB |
| 行数 | 10,225（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/sighting.parquet`） | 17（うち文字列 12） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `juveniles_text` 84.6%、`action` 76.1%、`adults_text` 73.0%、`others_text` 65.9% |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: sighting.parquet。他のファイルは未検査） |

## 答えうる問い

- 京都府のクマ目撃の環境（集落内・路上・畑・林など）別の分布（2018年まで）

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字 | BOM つき UTF-8の CSV。環境区分（`集落内`、`路上`、…）が日本語で読める | — |
| 検証 | CSV と全行・全列を照合したとカードが述べる | — |
| 時点 | — | FY2009〜FY2018（2018年12月まで）のみ。カタログは2022-04-18以降更新されていない。新しい記録は無い |
| 年ごとの差 | — | 年ごとの件数が8倍近く違う（2009年239、2010年1,975…）。収集方法は元が書かない |
| 型 | — | 頭数がテキスト（`others_text` に `不明` 100行と、頭数でない文1行）。数字の末尾の空白は取り除いてある。67の項目に改行が残る |
| 重複 | — | 場所・座標・日付が同じ記録の組が101（残してある）。最頻の場所は舞鶴市字三浜（48件、同じ座標） |
| 欠損(実測) | — | `others_text` 66%、`individual_status` 57%、`action` 76%がnull |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/kyoto-bear-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/kyoto-bear-sighting?blobs=true`）と Parquet フッターの取得（2026-10-26）
