---
id: yuiseki-datasets-text-corpora
title: テキストを主とするデータセットの読み方：PDF 由来、wikitext 由来、スキャン由来、法令
status: draft
sources:
  - yuiseki/ 配下の gsj-reports、nilim-disaster-reports、mlit-river-basin-overviews、moni1000-reports、rinya-forest-inventory、egov-laws-jp、un-docs、osm-wiki、wikipedia-geotagged、wikivoyage-geotagged、wikidata-gazetteer のカード（2026-10-24 取得）
  - Parquet の先頭3,000行の文字検査（2026-10-24）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related:
  - yuiseki-datasets-rights-exclusions
  - yuiseki-datasets-scale
verified_how: read-data
pattern: pattern
finding:
  - テキスト系の品質は、元の媒体（PDF の文字層、スキャン OCR、wikitext、XML）で決まる。U+FFFD が無いことは、文章が正しいことを意味しない
---

## 要点

- テキスト系は、地物系に比べて「文字コード」より「元の媒体から本文をどう取ったか」が品質を決める。

## 媒体ごとの読み方（カードの記述）

| 媒体 | データセット | 作り方 | 問題がない（意味） | 問題がある（意味） |
|---|---|---|---|---|
| PDF の文字層（pdftotext -layout） | gsj-reports、nilim-disaster-reports、mlit-river-basin-overviews、moni1000-reports、rinya-forest-inventory | 1ページ1行の JSONL。PDF の出典 URL とハッシュつき（gsj は SHA-256 を持つ） | 元 PDF を再取得して検証できる | 2段組の左右が1行に並ぶ。見出し・ページ番号・キャプション・表の桁揃えが混ざる。古い号は OCR 層の誤認識を含み、U+FFFD が無くても正しいとは限らない |
| スキャン（OCR） | un-docs | 文書39,363件のうち1,864件を tesseract で読んだ | テキスト層のある37,499件は元の文字をそのまま使う | OCR 誤りを含みうる。先頭3,000行中2行に U+FFFD（実測） |
| wikitext | osm-wiki、wikipedia-geotagged、wikivoyage-geotagged | テンプレートを展開・平文化 | タグの表のセルなど、内容を残す作り（osm-wiki） | リダイレクトは除外。場所でない記事を含む（英語 Wikipedia の6.1%、Wikivoyage の3.3%）。osm-wiki は先頭3,000行中1行に U+FFFD（実測） |
| 法令 XML | egov-laws-jp | XML の本文ノードを改行で連結 | 構造が必要なら同じ行の XML を読める | 改正版ごとに全文のコピーがあり、大きな法律が支配的になる。別表は語の断片になる |
| Wikidata | wikidata-gazetteer | P625/P1566 を持つ全項目 | CC0 | 言語・人物など場所でないものが入る。日本語名は4.0%のみ |

## 使うときの注意（意味づけ）

- **学習用コーパスとして**: gsj-reports 等はカード自身が「整形済みの学習用テキストではない」と書く。重複版（egov-laws-jp）や場所でない記事（Wikipedia 系）を除く処理を、使う側で行う。
- **権利**: 公的機関の文書でも、共同刊行・図表の他者クレジットがあり、一部は除外されている（`yuiseki-datasets-rights-exclusions`）。
- **規模**: wikipedia-geotagged は英語43億字・日本語4.35億字で、日本語を主に使う用途では日本語サブセットだけで足りる。

## 確かめなかったこと

- 先頭3,000行以外の文字の質、OCR の誤り率は測っていない。
- テキストの内容の正しさ（事実関係）は検証していない。

## 出典

- 上記データセットのカード、Parquet の文字検査（2026-10-24）
