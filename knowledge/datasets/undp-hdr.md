---
id: undp-hdr
title: undp-hdr で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/undp-hdr のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット dfc80c7、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - worldbank-wdi
  - unhcr-refugee-stats
dataset: yuiseki/undp-hdr
verified_how: read-data
pattern: questions
finding:
  - 人間開発指数(HDI)とGDI・IHDI・GII・PHDI、構成要素、統計付録表、多次元貧困指数(MPI)
---

## 要点

- 人間開発指数(HDI)とGDI・IHDI・GII・PHDI、構成要素、統計付録表、多次元貧困指数(MPI)。195か国・11集計行、1990〜2023年。横持ち(1,112列)と縦持ち。
- 分類: 世界の統計。元の情報源: 国連開発計画 人間開発報告(2025年版データ)。
- 権利: CC BY 3.0 IGO。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット dfc80c7（最終更新 2026-10-05、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 5.3 MB、ファイル 17 本 |
| Parquet | 2 本、合計 2.6 MB、最大 1.5 MB |
| 行数 | 200,210（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/hdr2025/composite_indices.parquet`） | 1112（うち文字列 4） |
| 行グループ数（標本の最大） | 2 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| ほぼ空の列（代表ファイル） | `gdi_1990` 62.6%、`hdi_f_1990` 62.6%、`hdi_m_1990` 62.6%、`hdi_m_1992` 61.7% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: composite_indices.parquet、composite_indices_long.parquet。他のファイルは未検査） |

## 答えうる問い

- 国別のHDIと構成要素の推移
- 不平等調整・ジェンダー指標の比較

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | 元 CSV は Windows-1252 で、Parquet は UTF-8 で読めるとカードが検証 | — |
| 検証 | 横持ち表の全セル(229,072)が CSV と一致 | — |
| 行の種類 | — | 206行のうち11行は集計(`iso3` が `ZZ` で始まる)。国だけにするには除く |
| 列の多さ | — | 横持ちは1,112列。指標×年が列名に入る |
| 改訂 | — | 毎年、全系列を計算し直す。年次を混ぜない |
| HDI なし | — | 北朝鮮・モナコはHDIが無い |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/undp-hdr のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/undp-hdr?blobs=true`）と Parquet フッターの取得（2026-10-24）
