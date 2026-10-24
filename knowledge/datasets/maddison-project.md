---
id: maddison-project
title: maddison-project で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/maddison-project のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット d424892、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - pwt
  - worldbank-wdi
dataset: yuiseki/maddison-project
verified_how: read-data
pattern: questions
finding:
  - 西暦1年から現在までの一人当たり実質GDPと人口
---

## 要点

- 西暦1年から現在までの一人当たり実質GDPと人口。3リリースを、それぞれ公表のまま、型付き Parquet と原本(Stata・xlsx・PDF)で保持。
- 分類: 世界の統計。元の情報源: Maddison Project Database 2018・2020・2023(GGDC)。
- 権利: CC BY 4.0(各版が求める引用つき)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット d424892（最終更新 2026-10-05、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 27.2 MB、ファイル 25 本 |
| Parquet | 6 本、合計 0.6 MB、最大 0.2 MB |
| 行数 | 191,757（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/2023/full_data.parquet`） | 6（うち文字列 3） |
| 行グループ数（標本の最大） | 2 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `pop` 86.4%、`gdppc` 83.7% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 国別の長期成長
- 版による推計の違い

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 検証 | xlsx を標準ライブラリだけで読み直し、行数と値が一致するとカードが検証 | — |
| 版をまたげない | — | 3版は系列の定義が違い、積んで1つの表にできない |
| ラベル | — | 2018年の凡例(0/1/2、コード1〜5)と実際のセルのラベルが違う。空文字は NULL にせず空文字のまま |
| 余白行 | — | 2018年のシートに書式だけの空行126行があり、Parquet からは除いてある |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/maddison-project のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/maddison-project?blobs=true`）と Parquet フッターの取得（2026-10-24）
