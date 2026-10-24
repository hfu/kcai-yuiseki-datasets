---
id: estat-boundary-2020
title: 国勢調査の小地域境界（2020）は、人口を結ぶための基盤になるか
status: draft
sources:
  - yuiseki/study-geoai-algo-py docs/datasets/estat-boundary/README.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - estat-boundary-2020-duplicate-boundaries
  - jp-admin-2026-09
verified_how: read-card
pattern: questions
finding:
  - 小地域境界は「人口の表」と「境界の面」を一緒に持つので、地理結合の基盤として使いやすい
---

## 要点

- このデータセットが答えうる問いの本体は、「どの小地域にどの人口があるか」「どの形を持つか」「どこまで同じ境界か」を扱うこと。
- ただし、人口の集計値は国勢調査の表全体ではなく、境界データの属性の一部に限られるので、単独では年齢別・世帯構成・就業の問いには弱い。
- 行政区域との結合や、他の統計テーブルとの結合に向く。
- 複数行が同じ KEY_CODE を持つ仕様を前提にしないと、人口の合計がずれる。

## 答えうる問いの例

- 小地域ごとの人口と世帯数を、行政区域コードと結びつけて表にする
- どの小地域が「面積最大の境界」かを見つける
- 市区町村ごとの境界の重なりや分割を確認する

## 答えられそうで答えられない問い

- 小地域ごとの全ての属性を、国勢調査統計表のように完全に再現することは難しい
- 町丁・字等境界の定義と、統計表の集計単位が完全に一致しない場合がある

## つまずきやすいところ

- 重複境界の扱い
- `KEY_CODE` と `PREF + CITY + S_AREA` の違い
- `HCODE` による「町丁・字等」と「水面調査区」の違い

## 出典

- yuiseki/study-geoai-algo-py docs/datasets/estat-boundary/README.md（コミット 6880b32）
