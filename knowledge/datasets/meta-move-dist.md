---
id: meta-move-dist
title: meta-move-dist で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/meta-move-dist のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット a37d917、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - meta-range-maps-2022-05
  - mlit-1km-fromto-2022-01
dataset: yuiseki/meta-move-dist
verified_how: read-data
pattern: questions
finding:
  - 217か国の行政区×日ごとに、ふだんの居場所から離れた距離の割合(0km・10km未満・10〜100km・100km超)
---

## 要点

- 217か国の行政区×日ごとに、ふだんの居場所から離れた距離の割合(0km・10km未満・10〜100km・100km超)。HDX の90日制限を超えて保持。
- 分類: 世界の地理。元の情報源: Meta Data for Good Movement Distribution(HDX、2026-06-01〜)。
- 権利: CC BY 4.0(Meta と HDX のクレジット)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット a37d917（最終更新 2026-10-02、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 1.03 GB、ファイル 19 本 |
| Parquet | 1 本、合計 89.1 MB、最大 89.1 MB |
| 行数 | 11,735,260（全 Parquet のフッターの合計） |
| 列数（代表ファイル `movement-distribution/movement_distribution_2026.parquet`） | 8（うち文字列 5） |
| 行グループ数（標本の最大） | 117 |
| GeoParquet の `geo` メタデータ | なし（代表ファイル） |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- 移動距離の時系列と地域差

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 規模 | Parquet 1本(89MB、1,173万行、117行グループ) | — |
| 欠測日 | — | 2026年8月は16日分がどのファイルにも無い。ファイル名でなく `ds` 列を信頼する |
| 重複 | — | ファイルの端で日が重なる(617,668行)。値は同じで、HDX が最後に更新したファイルから1回だけ残してある |
| 分割 | — | 6月の4ファイルは日でなく行数で切られている |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/meta-move-dist のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/meta-move-dist?blobs=true`）と Parquet フッターの取得（2026-10-24）
