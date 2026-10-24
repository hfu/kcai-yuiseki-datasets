---
id: yuiseki-datasets-patterns-regional-keys
title: 地域コードと時点をつなぐ共通パターン
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/jp-admin-2026-09.md（コミット 6880b32）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/abr-src-2026-09.md（コミット 6880b32）
  - yuiseki/study-geoai-algo-py docs/datasets/geoboundaries/README.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-japan-admin-lineage
  - estat-boundary-2020-duplicate-boundaries
verified_how: read-docs
pattern: pattern
finding:
  - 日本の地域コードで結ぶ前に、コードの桁数・型・時点・粒度の組を明示する。Yuiseki さんのカードに、桁の違い、ゼロ落ち、時点のずれ、名前照合の率が具体的に書かれている
---

## 要点

- コードは文字列で持つ。estat-boundary-2020 の属性は全部 VARCHAR で、CITY は `402` のような 3 桁。型推論で数値にすると結合が壊れる。abr-src-2026-09 も、`lg_code 011011` や `machiaza_id 0000101` の先頭のゼロを守るため全列 VARCHAR。
- 桁が違うコードを同じ名前で呼ばない。`KEY_CODE` は 11 桁（152,442 行）、9 桁（79,489 行）、2 桁（88 行）が混在し、PREF+CITY+S_AREA と一致しない行が 79,577 ある。小地域キーは PREF+CITY+S_AREA の 11 桁を自分で作るほうが安全（estat-boundary-2020 のカード）。
- 市区町村までは `PREF+CITY`＝`lg_code` の先頭 5 桁（`code5`）で結べる。町字は共通キーが無く、名前の照合になる（カードは 77.0%、東京 95.8% と書く。測っていない）。
- 時点が混ざる。jp-admin-2026-09 は名前とコードが 2026-09 時点、ポリゴンと人口が 2020 年。浜松市の 3 区は名前だけで形が無い。abr-src は同じ 1 つのデータセットの中でも、町字の名前 2026-09-25、町字の代表点 2025-10-27、都道府県と市区町村 2024-03 と版が違う。
- 「同じ粒度」と呼ぶ名前を信じない。geoboundaries の日本の ADM2 は canonical が Subprefectures だが件数は 1,745 で、市区町村（1,741）に近い。`boundaryCanonical` は出どころの自称で、国をまたいで同じ粒度とは限らない。

## 結合の組と、カードが書く結び方

| 結ぶもの | 結び方 | 注意 |
|---|---|---|
| estat-boundary-2020 ↔ jp-admin-2026-09 | jp-admin が estat から作られている。provenance.yaml がコミット 823195c を固定 | 人口は政令市の区と市の両方が行にある |
| jp-admin ↔ abr-src | jp-admin のコード・名前・代表点は abr 由来 | 北方領土 6 村の代表点は全て同じ点 |
| estat-boundary-2020 ↔ abr-src（町字） | 名前の照合のみ | abr の `cns_bnd_s_area_kcode` は全行空で、コードでは結べない |

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md、jp-admin-2026-09.md、abr-src-2026-09.md（いずれもコミット 6880b32）
- yuiseki/study-geoai-algo-py docs/datasets/geoboundaries/README.md（コミット 6880b32）
