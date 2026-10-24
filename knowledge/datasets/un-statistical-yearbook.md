---
id: un-statistical-yearbook
title: un-statistical-yearbook で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/un-statistical-yearbook のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 201d1ce、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - undata-sdmx
  - worldbank-wdi
dataset: yuiseki/un-statistical-yearbook
verified_how: read-data
pattern: questions
finding:
  - 国連統計年鑑の表(SYB68 の32表、SYB61 の1表)
---

## 要点

- 国連統計年鑑の表(SYB68 の32表、SYB61 の1表)。出典機関ごとに権利を見て、再配布できる行だけを Parquet 24本にした。
- 分類: 世界の統計。元の情報源: 国連統計部 UNdata「統計年鑑」の表。
- 権利: UNdata の規約と出典機関の規約。再配布できる行だけ(22表105,902行)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 201d1ce（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 22.9 MB、ファイル 50 本 |
| Parquet | 24 本、合計 0.4 MB、最大 0.0 MB |
| 行数 | 105,976（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/syb68/327_international_migrants_and_refugees.parquet`） | 7（うち文字列 4） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: 327_international_migrants_and_refugees.parquet、sources.parquet。他のファイルは未検査） |

## 答えうる問い

- 国・地域別の人口、国民経済計算、教育、貿易、エネルギー、環境、ICT の横断比較

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | 元 CSV は Windows-1252 で、厳密にデコードできるとカードが検証 | — |
| 権利除外 | — | WHO、ITU、IMF、IUCN、UNODC、UN Tourism、WIPO、IPU、UNEP-WCMC の行は除外。表が欠ける・行が減る |
| 行の種類 | — | `area_code` は M49。国・地域・集計(`LDC§` のように印つきの名前も)が混ざる。0 は「合計」 |
| 単位 | — | 1表に複数の系列(`series`)がある。絞ってから比べる |
| 脚注 | — | 43,395/105,902行に脚注があり、値の意味を変えうる |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/un-statistical-yearbook のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/un-statistical-yearbook?blobs=true`）と Parquet フッターの取得（2026-10-24）
