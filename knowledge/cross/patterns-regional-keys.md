---
id: yuiseki-datasets-patterns-regional-keys
title: 地域コードと時点をつなぐ共通パターン
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/README.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related: []
verified_how: read-card
pattern: pattern
finding:
  - 地域コードをそのままキーにしてしまうと、境界変化やコードの変遷で結合が壊れるため、時点と粒度を明示する必要がある
---

## 要点

- 地域コードは便利なが、境界や町名の変遷により、時点ごとに不一致が起きる。
- 同じ市区町村でも、統計年と境界年が違うと、表と地物の結合がずれる。
- こうしたつまずきは、`PREF + CITY` のような集合でキーを作るよりも、年と境界の情報を別に持つことが安全。

## 例

- 国勢調査の小地域境界と行政区画コードの結合
- 統計表の市区町村コードと境界データの市区町村コードの結合

## 実務上の視点

- まず「地理的な単位」を決める
- 次に「時点」を決める
- そのうえで「識別子」を選ぶ

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/README.md（コミット 6880b32）
