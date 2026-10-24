---
id: jp-admin-2026-09
title: 市区町村コードと境界の基盤データ
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/jp-admin-2026-09.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - estat-boundary-2020
verified_how: read-card
pattern: questions
finding:
  - 市区町村行政区画は、境界データと統計データをつなぐキーとして使いやすい
---

## 要点

- 行政区画のコードと境界は、全国の単位で比較できる。
- 市区町村ごとの情報を集計する場合、境界と統計を結ぶときの基盤として働く。
- ただし、国勢調査の小地域境界とは粒度が違うので、直接 1:1 で結ぶには注意が必要。

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/jp-admin-2026-09.md（コミット 6880b32）
