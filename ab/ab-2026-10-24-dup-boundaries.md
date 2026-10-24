---
question: |
  2020 年国勢調査の小地域境界データ（yuiseki/estat-boundary-2020）を使って、小地域ごとに一行で人口と形を持つ表を作りたい。どう作ればよいか。
without_trail: |
  「KEY_CODE が重複している行を削って、残りの人口を足していけばよい」と考える。代表の形は `AREA_MAX_F = 'M'` の行を使う。
with_trail: |
  まず `KIGO_E` が空か E1 の行を人口の本体として選び、`AREA_MAX_F = 'M'` の行を代表形の候補として見る。ただし `M` が E2 以降のときは人口が 0 なので、人口の意味と形の意味が別の行にあることを踏まえる。
correct_answer: with_trail
judgement: |
  e-Stat の定義書と Yuiseki さんの踏み跡の双方で、重複境界の説明と E1 / M の違いが一致している。重複行を消すと人口の欠落や誤差が起きるため、with_trail の方が正確である。
---

## 要点

- 小地域の重複行は「誤り」ではなく、仕様のなかでの分割境界の別表現である。
- 人口と世帯数の値は E1 の行に入るので、重複行を消して足すと人口が失われる。
- 代表形の決定には `AREA_MAX_F = 'M'` を使うが、M 行が人口の本体ではないことがある。

## 結論

この問いに対して、踏み跡ありの答えが正しい。境界データの重複は「データの欠陥」ではなく仕様であり、人口と形の代表値は別の行から取る必要がある。

## 根拠

- `knowledge/datasets/estat-boundary-2020-duplicate-boundaries.md`
- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
- 総務省統計局 e-Stat「令和２年国勢調査 町丁・字等境界データ データベース定義書」

## 出典

- `knowledge/datasets/estat-boundary-2020-duplicate-boundaries.md`
- yuiseki/study-geoai-algo-py docs/datasets/huggingface-yuiseki/estat-boundary-2020.md（コミット 6880b32）
- 総務省統計局 e-Stat「令和２年国勢調査 町丁・字等境界データ データベース定義書」
