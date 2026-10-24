---
id: estat-boundary-2020-duplicate-boundaries
title: 国勢調査の小地域境界（2020）で、同じ小地域が複数行になる理由と、人口の正しい数え方
status: draft
sources:
  - 総務省統計局 e-Stat「令和２年国勢調査 町丁・字等境界データ データベース定義書」 https://www.e-stat.go.jp/help/data-definition-information/downloaddata/A002005212020.pdf
  - yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
authors:
  - hfu（AI 支援あり）
reviewed_by: []
updated: 2026-10-24
related: []
dataset: yuiseki/estat-boundary-2020
verified_how: read-docs
pattern: re-walk
finding:
  - Yuiseki さんの踏み跡で「未確認」だった KIGO_E、AREA_MAX_F、HCODE 8154 の意味を、e-Stat の定義書で確かめた
---

## 要点

- 同じ KEY_CODE が複数の行に現れるのは、定義どおりの仕様である。一つの市区町村の中で、同じ町丁・字等の番号を持つ境界が複数あるとき、`KIGO_E` に E1、E2、… が付く。
- 人口、世帯数、基本単位区の数は E1 の行だけに入り、E2 以降の行は 0 になる。だから、行ごとに足しても二重計上にはならない。
- 小地域ごとに一行にしたいときは、統計の値は E1 の行（`KIGO_E` が空の行を含む）から、いちばん大きな形は `AREA_MAX_F = 'M'` の行から取る。E1 は人口の順、M は面積の順で決まるので、両者は同じ行とは限らない。
- `HCODE` の 8154 は「水面調査区」で、8101 の「町丁・字等」とは別の扱いになる。

## 詳しく

データセットの列や件数は、Yuiseki さんの踏み跡にある。ここでは、そこで「未確認」だった項目の意味だけを、定義書で確かめた結果として書く。

| 項目 | 定義書による意味 |
|---|---|
| `KIGO_E` | 町丁・字等重複フラグ。同じ番号の境界が複数あるとき E1、E2、… を付ける。番号は、集計した人口の順、次に面積の順で付け、陸地を島より優先する |
| `AREA_MAX_F` | 面積最大フラグ。重複した境界のうち面積が最大のもの、または重複がない境界に M を付ける |
| `KBSUM` | 基本単位区・調査区の数。重複があるときは E1 に入れ、E2 以降は 0 |
| `HCODE` | 分類符号。8101 は町丁・字等、8154 は水面調査区 |

Yuiseki さんの実測（行数と KEY_CODE の数の差、人口の合計が公表値と一致すること、東京で `AREA_MAX_F` が空の行にも人口が入っていたこと）は、この定義と矛盾しない。最後の観察は、「E1 は人口の順、M は面積の順」で説明がつく。人口が最も多い部分と、面積が最も大きい部分が、別の行になる小地域がある。

## よくあるまちがい

- KEY_CODE の重複を「データの誤り」と考え、重複を消してから人口を足す。消し方によっては E1 の行を落とし、人口を失う。
- 小地域を一行にするときに、`AREA_MAX_F = 'M'` の行の人口を使う。M の行が E2 以降なら、人口は 0 になる。
- 人口密度を求めるときに、水面調査区（8154）を含めるかどうかを決めずに計算する。

## この踏み跡で答えられるようになる問い

- 小地域ごとに一行で、人口と代表の形を持つ表を作るには、どうすればよいか。
- 人口が最も多い部分と、面積が最も大きい部分が別の行になる小地域は、どこか。

## 確かめなかったこと

- E1 の行と M の行が、実際にどれくらいの数の小地域で食い違うか。データそのものを読んで数える必要がある（この踏み跡を書いたセッションからは、Hugging Face のデータに届かなかった）。

## 出典

- 総務省統計局 e-Stat「令和２年国勢調査 町丁・字等境界データ データベース定義書」 https://www.e-stat.go.jp/help/data-definition-information/downloaddata/A002005212020.pdf
- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
