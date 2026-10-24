---
id: yuiseki-datasets-japan-admin-lineage
title: 日本の行政区画データの連鎖：estat-boundary-2020 → jp-admin ← abr-src → geo-triples-jp-gov
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/jp-admin-2026-09.md（コミット 6880b32）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/abr-src-2026-09.md（コミット 6880b32）
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/geo-triples-jp-gov.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-patterns-regional-keys
  - yuiseki-datasets-landscape
verified_how: read-card
pattern: pattern
finding:
  - 日本の行政区画の 4 データセットは派生の連鎖で、どれを起点にするかで粒度（小地域・市区町村・町字）と時点が決まる
---

## 要点

```
e-Stat 小地域境界（2020） ─→ estat-boundary-2020 ─┐ ポリゴン・人口
デジタル庁 ABR（2026-09） ─→ abr-src-2026-09 ────┴→ jp-admin-2026-09 ─→ geo-triples-jp-gov
                                    コード・名前・代表点        （隣接・包含の三つ組）
```

| 知りたいこと | 起点 | 理由 |
|---|---|---|
| 小地域（町丁・字等）の人口と形 | estat-boundary-2020 | 232,019 行、人口の合計が公表総人口 126,146,099 と一致。重複行の読み方は `estat-boundary-2020-duplicate-boundaries` |
| 市区町村の表（コード・名前・人口・形） | jp-admin-2026-09 | 1 行 1 市区町村。政令市は本体と区が両方行 |
| 町字の名前・読み・代表点 | abr-src-2026-09 | 境界と人口は無い |
| 市区町村の隣接・包含 | geo-triples-jp-gov | `sfTouches` などの述語で、入力は jp-admin の 1,909 件 |

## 結合の注意

- 市区町村までは `PREF+CITY`＝`lg_code` 先頭 5 桁で結べる。町字は名前の照合のみ（abr 側の国勢調査キーは全行空）。
- 起点が違えば時点も違う: 人口は 2020 年、コードと名前は 2026-09、abr の代表点は 2025-10。「現在の市区町村に 2020 年の人口を載せる」ので、合併・新設（浜松市の 3 区など）で欠ける行が出る。
- 1,918（jp-admin）、1,909（geo-triples の入力）、1,897（estat の PREF+CITY の種類）、1,747（区を除く）と、同じ「市区町村」の数が文脈で違う。数を引くときは何の数かを添える。

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/ の上記 4 カード（コミット 6880b32）
