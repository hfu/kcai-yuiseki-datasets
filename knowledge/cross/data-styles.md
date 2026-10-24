---
id: yuiseki-datasets-data-styles
title: データスタイルの違いと、その扱い方の案
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md、jp-admin-2026-09.md、abr-src-2026-09.md（コミット 6880b32）
  - yuiseki-datasets-access-methods（2026-10-24 の実測）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-access-methods
  - yuiseki-datasets-scale
verified_how: read-docs
pattern: styles
finding:
  - 形・空間単位・識別子の扱いの違いは、データをつなぐ際の主要な障害になる
---

## 要点

- 形の種類が違う: 点、線、面、表、文、画像、メッシュ。
- 空間単位の違い: 行政区域・小地域・市区町村・メッシュ・タイル・施設・道路・国境。
- 表記の違い: 文字列と数値、空欄と 0 の扱い、地域コードの長さとゼロ埋め。
- 時点の扱い: 凍結版と上書き型のデータが混在する。

## 典型的な差分の例

- 境界データは「面」だが、行政統計は「表」だと見なせる。
- 住所データは「点」だが、境界データと結ぶときは名前やコードの照合が必要になる。
- コードは `PREF + CITY + S_AREA` の組合せ、あるいは市区町村コード単体など、粒度が違う。
- `JINKO` や `SETAI` のように値が数値なのか、文字列に変換されているのかも、結合設計に効く。

## 問いに対する観点

- 結合しやすいのは、同一の空間単位と同一の識別子を持つ組み合わせ。
- そうでないときは、地域名の変動、統計年と境界年の差、重複境界と代表形の選定が問題になる。
- したがって、データ選定の前に「どの粒度で結ぶか」を決めるのが重要である。

## 追加: 文字コードと幾何の持ち方（2026-10-24 の実測）

- 日本語属性: Hugging Face の Parquet は UTF-8 で、estat-boundary-2020、jp-admin、abr-src とも日本語が正しく読めた。元の配布物（e-Stat の Shapefile は cp932）の文字コードの問題は、Parquet を使えば避けられる。
- 幾何: GeoParquet の `geo` メタデータがあるものと無いものが混在する（`yuiseki-datasets-access-methods`）。メタデータが無いと、terrio 0.4.2 は WKB の列を幾何と認識しなかった。
- コードの型: abr-src は全列が文字列（先頭のゼロを守る）、estat-boundary-2020 も属性は全部文字列、jp-admin は人口などが数値型。

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/ の estat-boundary-2020.md、jp-admin-2026-09.md、abr-src-2026-09.md（コミット 6880b32）
