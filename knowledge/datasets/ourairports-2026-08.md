---
id: ourairports-2026-08
title: ourairports-2026-08 で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/ourairports-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット 6c1d115、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - osm-japan-src-2026-08
  - natural-earth
dataset: yuiseki/ourairports-2026-08
verified_how: read-data
pattern: questions
finding:
  - 空港・ヘリポート・飛行場86,002件と滑走路・周波数・航法援助
---

## 要点

- 空港・ヘリポート・飛行場86,002件と滑走路・周波数・航法援助。IATA/ICAO コード、定期便の有無。CSV 7本と型付き Parquet。
- 分類: 世界の地理。元の情報源: OurAirports(2026-08末のコミット)。
- 権利: パブリックドメイン(LICENSE は Unlicense でソフトウェア向けの文言)。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット 6c1d115（最終更新 2026-10-02、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 33.3 MB、ファイル 19 本 |
| Parquet | 7 本、合計 8.6 MB、最大 5.0 MB |
| 行数 | 196,198（全 Parquet のフッターの合計） |
| 列数（代表ファイル `parquet/airports.parquet`） | 20（うち文字列 16） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `home_link` 94.5%、`iata_code` 89.5%、`icao_code` 87.8%、`wikipedia_link` 80.5% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | 異常なし |

## 答えうる問い

- IATA・ICAO コードから空港を引く
- 国・地域別の空港数

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | 点の GeoParquet | — |
| 内容 | — | 多くは空港でない(小規模飛行場42,707、ヘリポート23,196、閉鎖13,482) |
| 型 | — | 型は列名から決めてある。`regions.local_code` のように引用符の無いゼロつきコードは、推論に任せると数値化される |
| 形 | — | 形は点のみ。滑走路ポリゴンや駅舎は OSM |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 全ファイルの全行を対象にした検査はしていない（上の表の範囲のみ）

## 出典

- yuiseki/ourairports-2026-08 のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/ourairports-2026-08?blobs=true`）と Parquet フッターの取得（2026-10-24）
