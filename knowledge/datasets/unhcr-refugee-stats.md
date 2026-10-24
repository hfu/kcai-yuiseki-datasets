---
id: unhcr-refugee-stats
title: unhcr-refugee-stats で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/unhcr-refugee-stats のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 5f3eea4、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - undp-hdr
  - ucdp-ged
dataset: yuiseki/unhcr-refugee-stats
verified_how: read-data
pattern: questions
finding:
  - 難民・庇護申請者・国内避難民・無国籍者などの、出身国×庇護国×年の人数、庇護の申請と決定、帰還・再定住・帰化、年齢性別内訳
---

## 要点

- 難民・庇護申請者・国内避難民・無国籍者などの、出身国×庇護国×年の人数、庇護の申請と決定、帰還・再定住・帰化、年齢性別内訳。5系統+国表。
- 分類: 世界の統計。元の情報源: UNHCR Refugee Population Statistics Database(API、2026-10-04取得)。
- 権利: CC BY 4.0(第三者データのIDMC・UNRWAは除外)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 5f3eea4（最終更新 2026-10-05、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 7.2 MB、ファイル 18 本 |
| Parquet | 7 本、合計 2.6 MB、最大 1.0 MB |
| 行数 | 512,348（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/2026-10-04/demographics.parquet`） | 20（うち文字列 4） |
| 行グループ数（標本の最大） | 2 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 出身国・庇護国ごとの人数の推移
- 庇護申請の認定率

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | 行数が API の申告値と一致、全値の sha256 が原本と一致するとカードが検証 | — |
| 丸め | — | 5未満は5の倍数に丸められ、庇護決定は5〜10に丸められる。表間の合計は近似 |
| 欠測 | — | `-` は 0 ではなく NULL。「その他の保護対象者」は2018年以前ほぼ全行が `-` |
| 改訂 | — | 同じ年の数値が後の版で変わる |
| 範囲 | — | 第三者データ(IDMC、UNRWA)は含まれない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/unhcr-refugee-stats のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/unhcr-refugee-stats?blobs=true`）と Parquet フッターの取得（2026-10-24）
