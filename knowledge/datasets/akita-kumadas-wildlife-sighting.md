---
id: akita-kumadas-wildlife-sighting
title: akita-kumadas-wildlife-sighting で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/akita-kumadas-wildlife-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
  - Hugging Face API と Parquet のフッター（コミット c7047ab、2026-10-26）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-26
related:
  - gifu-bear-sighting
  - ishikawa-bear-incident
  - kamisunagawa-higuma-sighting
  - kyoto-bear-sighting
  - nagaoka-bear-sighting
dataset: yuiseki/akita-kumadas-wildlife-sighting
verified_how: read-data
pattern: questions
finding:
  - クマダスの目撃・痕跡・人身被害の記録24,757件（2022-04-10〜2026-09-30）
---

## 要点

- クマダスの目撃・痕跡・人身被害の記録24,757件（2022-04-10〜2026-09-30）。ツキノワグマ23,306・イノシシ885・ニホンジカ566。場所（住所と緯度経度）・日時・獣種・群れ・頭数。元の CSV も併置。
- 分類: クマ出没記録。元の情報源: 秋田県「ツキノワグマ等情報マップシステム『クマダス』データ」（秋田県オープンデータカタログ、自然保護課、2026-09-30時点）。
- 権利: CC BY 4.0（カタログの記載）。出典「秋田県…を加工して作成」。

## 規模と形（2026-10-26 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット c7047ab（最終更新 2026-10-26、2026-10-26 に API で確認） |
| Hugging Face のライセンスタグ | cc-by-4.0 |
| 全体 | 8.5 MB、ファイル 9 本 |
| Parquet | 1 本、合計 2.1 MB、最大 2.1 MB |
| 行数 | 24,757（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/sighting.parquet`） | 13（うち文字列 7） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| 全行の文字検査（1 ファイル、全文字列列） | 異常なし（検査したファイル: sighting.parquet。他のファイルは未検査） |

## 答えうる問い

- 秋田県のクマの出没の時期・場所の分布（報告ベース）
- 人身被害の記録の抽出

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 文字コード | 元の CSV は BOM つき UTF-8。日本語の `info_type`（`人身被害`、`痕跡(その他)`、`痕跡(食害)`、`目撃`）が読める | — |
| 検証 | Parquet は別の CSV リーダーで全行・全列を照合したとカードが述べる | — |
| 幾何 | 点の GeoParquet 1.1.0。全点が秋田県の範囲内（カード） | — |
| 混在 | — | クマ・イノシシ・ニホンジカが1つの表にある。クマだけにするには `species` で絞る |
| 意味 | — | 報告であり、同じ個体が何度も報告されうる。頭数は個体数調査ではない。位置の精度は元が示さない |
| 欠番 | — | 出没情報IDは1〜28054だが記録は24,757件で、3,297のIDが無い（理由は元が書かない）。「【投稿】」の記録1,003件（住民の投稿とみられるが未確認） |
| 時点 | — | 毎月上書きされる元の、2026-10-26の状態のみ |
| 座標系 | — | 元は測地系を示さず、CRS を書かない（WGS 84 既定） |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/akita-kumadas-wildlife-sighting のデータセットカード（README、Hugging Face 上の main、2026-10-26 取得）
- Hugging Face API（`/api/datasets/yuiseki/akita-kumadas-wildlife-sighting?blobs=true`）と Parquet フッターの取得（2026-10-26）
