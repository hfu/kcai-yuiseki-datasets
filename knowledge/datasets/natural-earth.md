---
id: natural-earth
title: natural-earth で何が答えられ、どの意味で問題がなく、どの意味で問題があるか
status: draft
sources:
  - yuiseki/natural-earth のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
  - Hugging Face API と Parquet のフッター（コミット efdd066、2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - ne-admin0-10m
  - geonames
dataset: yuiseki/natural-earth
verified_how: read-data
pattern: questions
finding:
  - 国・州・境界線・居住地・道路・鉄道・空港・港・時間帯・海岸線・河川など215レイヤーを、レイヤーごとの GeoParquet と元 zip で提供
---

## 要点

- 国・州・境界線・居住地・道路・鉄道・空港・港・時間帯・海岸線・河川など215レイヤーを、レイヤーごとの GeoParquet と元 zip で提供。ラスタ52 zip(約7.5GB)は含まない。
- 分類: 世界の地理。元の情報源: Natural Earth v5.1.2(1:10m・50m・110m の全ベクタ215レイヤー)。
- 権利: パブリックドメイン。

## 規模と形（2026-10-24 の実測）

| 項目 | 値 |
|---|---|
| 取得した版 | コミット efdd066（最終更新 2026-10-06、2026-10-24 に API で確認） |
| Hugging Face のライセンスタグ | other |
| 全体 | 1.28 GB、ファイル 427 本 |
| Parquet | 215 本、合計 450.3 MB、最大 50.7 MB |
| 行数 | 357,763（全 215 本のフッターの合計） |
| 列数（代表ファイル `parquet/v5.1.2/10m_cultural/ne_10m_admin_1_states_provinces_lakes.parquet`） | 122（うち文字列 36） |
| 行グループ数（標本の最大） | 1 |
| GeoParquet の `geo` メタデータ | あり（代表ファイル） |
| ほぼ空の列（代表ファイル） | `FCLASS_ISO` 100.0%、`FCLASS_US` 100.0%、`FCLASS_AR` 100.0%、`FCLASS_VN` 100.0% |
| 先頭行の文字検査（代表ファイルの先頭3,000行・文字列列） | `woe_label` U+FFFD 0行・二重エンコード疑い 91行；`woe_name` U+FFFD 0行・二重エンコード疑い 6行 |
| 全行の文字検査（2 ファイル、全文字列列） | 異常なし（検査したファイル: ne_10m_roads_north_america.parquet、ne_50m_admin_1_seams.parquet。他のファイルは未検査） |

## 答えうる問い

- 世界地図の背景としての境界・海岸線・居住地
- 国・州の紛争地の見え方(視点別レイヤー)

## 読み込みの観点：どういう意味で問題がなく、どういう意味で問題があるか

| 観点 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|
| 幾何 | GeoParquet。座標・形は再投影も修復もしていない | — |
| 分割 | レイヤーごとに1ファイル。必要な層だけ取れる | — |
| 文字コード | — | 元の DBF が二重エンコードされた文字(UTF-8 のバイトを Latin-1 と見て UTF-8 化したもの)を含む。例: `woe_label` の `PaysandÃº`。Parquet は元のまま保持している(下記の実測) |
| 時点 | — | Natural Earth は2022年5月から更新されていない |
| 視点 | — | 既定は事実上の境界で、視点別は別レイヤー |
| 不正形状 | — | 不正な幾何は数えて残してあり、直していない |

- 表のうち「実測」と書いていない項目は、データセットカードの記述を整理したもの（独立には検証していない）。「カードが検証」と書いたものは、カードに書かれた作者側の検証結果。

## 確かめなかったこと

- 215レイヤー全てでの二重エンコードの有無は未確認(確認した範囲は実測欄)
- 全215本のフッターの合計は357,763行で、カードの地物数と一致した

## 出典

- yuiseki/natural-earth のデータセットカード（README、Hugging Face 上の main、2026-10-24 取得）
- Hugging Face API（`/api/datasets/yuiseki/natural-earth?blobs=true`）と Parquet フッターの取得（2026-10-24）
