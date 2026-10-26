# un-docs の実測と「地理空間情報」の問いの試行（2026-10-26）

対象: yuiseki/un-docs `documents.parquet`（コミット 6cd1cf0、39,363 行）。duckdb（httpfs）で Hugging Face から直接読んだ。本文は 409MB の 1 ファイル。

## 集計に使った考え方

- 記号の型は、`id` の接頭辞（`A/RES/`、`S/RES/`、`S/PV.`、`S/PRST/`、`S/` に数字、`A/` に数字）で分けた。
- 安保理決議の番号は、`^S/RES/(\d+)\s*\((\d{4})\)` で取り、同じ番号の行を数えた。重複の本文が同じかは `md5(body)` で比べた。
- 日付は `coalesce(date_adopted, date_distributed, date_other)`。年は、日付が無ければ記号の `(YYYY)` か、`A/RES/N/` の会期 N から 1945+N とした。
- 語の検索は大文字小文字を区別せず、`geo-?spatial`、`geographic(al)?\s+information`、`remote\s+sensing`、`satellite\s+(imagery|image)`、`geodetic|geodesy` を `regexp_matches` で当てた。
- 「個別文書」は記号が `A/RES/`、`S/RES/`、`S/PRST/`、`S/PV.` で始まるもの。`A/NN/49(Vol.I)` のような合冊は除いた。

## 結果（要点のみ。全体は knowledge/cross/un-docs-kcai-feasibility.md）

- 本文が異なる行 36,835 / 39,363。
- S/RES 4,248 行 / 番号 2,699 通り（1〜2699）。2700〜2722 は無い。S/RES/2699 は 2023-10-02。
- S/PV 9,346 通り（最大 9436、90 欠け）、うち 1,970 に `votes in favour`。
- OCR 1,864 行のうち A/RES 1,532、S/PV 179。十年代別では 1980 年代 659/3,231、1990 年代 732/5,641。
- `geospatial`: 91 行 → 個別 37 件。初出 A/RES/61/111（2006-12-14）。年別（個別）は 2015 年が 7 件で最多。
- `geographic information`: 初出 A/RES/42/186（1987-12-11）。`remote sensing`: 2778(XXVI)。
- 「保護する責任」: 番号順の先頭は S/RES/1393（2002、通常の用法）。概念としての初出は S/RES/1674（2006）、A/RES/60/1。

## 注意と限界

- `GIS` を大文字小文字無視で検索すると、人名・地名の中の `gis` を拾う。結果から外した。`UN-GGIM` の同様の検索も、大文字小文字を区別して再確認した（個別文書では A/RES/69/266 のみ）。
- 年の推定が日付と記号で食い違う行がありうる。
- 公式サイト（docs.un.org）の原文との照合は、一部の引用（S/RES/1393、S/RES/1674、A/RES/60/1、A/RES/61/111）について、un-docs の抽出テキストの文言を読んだのみ。
