# hfu のレビュー・判断の待ち行列（2026-10-26 時点の叩き台）

全ての踏み跡は `status: draft`、`reviewed_by: []`。量が多い（97 件の個別 + 約 20 件の横断）ので、判断が分かれそうなもの・外部に影響しうるものから順に並べた。投稿・提案は hfu が行う（AI は行わない）。

## A. 先に読む横断の踏み跡（この順に 5 本）

1. `knowledge/cross/card-vs-data-checks.md` — カードと実データの食い違い、元データ由来の文字の欠陥。
2. `knowledge/cross/dataset-access-methods.md` — 置き方、`geo` メタデータ、terrio-js の実測（estat-boundary-2020 の実験、新規 11 本）。
3. `knowledge/cross/rights-exclusions.md` と `version-policies.md` — 除外された部分、版の持ち方。
4. `knowledge/cross/code-systems.md` — JIS・警察・FIPS・M49 など。変換表の有無は未確認。
5. `knowledge/cross/dataset-index.md` — 全 96 件の索引。分類（この踏み跡での整理）の妥当性。

## B. 外部への報告の候補（投稿するかは hfu の判断）

| 相手 | 内容 | 根拠 |
|---|---|---|
| yuiseki/estat-boundary-2020 | `geo` メタデータが無く、terrio 0.4.2 で幾何が null になる。`crs` を書かないと EPSG:4326 とみなされる。`bbox` 列と空間順の行グループで terrio-js の転送量が 6.9MB→0.66〜1.3MB | `checks/check-2026-10-24-estat-boundary-geoparquet.md` |
| yuiseki/geo-triples-japan | カード冒頭の件数が geo-triples-tokyo23 のもの（本文の表とデータは別の数） | `card-vs-data-checks` |
| yuiseki/geo-triples-tokyo23 | 冒頭は評価問題 8,890、本文・データは 8,854 | 同上 |
| yuiseki/natural-earth、ne-admin0-10m | 元の DBF が二重エンコード（`PaysandÃº`）。Parquet は忠実に保持。カードに注意書きが無い | 同上 |
| yuiseki/un-docs | 記号の綴りの重複（`S/RES/1 (1946)` と `S/RES/1(1946)`）、安保理決議が 2699 で切れる、OCR の説明の食い違い | kcai-un-docs 側の下書き |
| opengeos/terrio | Parquet の WKB 列を幾何と見ない（`Geometry: None` で黙って null）、CRS 無記載で 4326 とみなす、CP932 の Shapefile 属性が黙って化ける（0.3.2・0.4.2 とも） | `knowledge/cross/terrio-usage-possibilities.md`。kcai-terrio の `drafts/upstream/` が受け皿 |

## B'. 提案の候補（2026-10-31 追記）

| 相手 | 内容 | 根拠 |
|---|---|---|
| yuiseki の東北6県の現存植生図（`<県>-vegetation-2024`） | 1ファイル・1行グループ（129〜323MB）で、`covering` があっても小さな窓で全量を読む。Hilbert 順に並べた複数の行グループ（100〜250行／群）にすると、小さな窓の転送量が下がる見込み（estat-boundary-2020 の実験で約9〜19%） | `checks/check-2026-10-31-tohoku-range-reads.md`、`checks/check-2026-10-24-estat-boundary-geoparquet.md` |

## C. 判断が分かれる記述

- **worldpop-idn/kor のライセンス**: メタデータ名が `odbl-1.0-worldpop-cc-by-4.0-source`。既存の worldpop-jp は CC BY 4.0。理由（LICENSE に書かれた「保守的な選択」）は読んでいない。
- **gifu-bear-sighting の座標**: R2〜R7 は平面直角座標（`.prj` 無し）。カードは「第VII系（EPSG:6675）」と推定して投影し、3,236 点中 3,228 点が記録の市町村内に入ると述べる。推定は元が示さない。
- **ISHIKAWA の `remarks`** に U+FFFD が 17 行（原因は未確認）。
- **未確認のままの点**: un-wpp の 53 行の差、警察コードと JIS の変換表、`その他（自動）` の確認、130MB 超のファイルの文字検査。

## D. 品質の注意（レビューで効きそうな所）

- 「問題がない/ある」の表は、「実測」と書いたもの以外は**カードの記述を整理しただけ**。独立に確かめた範囲は、件数・列・欠損・文字の状態・`geo` メタデータ・（一部）範囲読み。
- kcai-un-docs 側の確かめ直しで、`un-docs-geospatial-institutions` の分類・要約に誤り（G5 サヘル関連の一般化、海洋法部の担当部署の断定、UNAMI の訓練の年、S/2005/673 の地図作成官の読み方など）が見つかり、訂正された。**他の横断の踏み跡にも、同種の「窓の文脈からの一般化」があるかもしれない**。特に `version-policies` の型の割り当てと、`rights-exclusions` の理由づけは、カードの該当節に戻って確かめる価値がある。
- 生成した 93 件（既存 66 + 新規 27）は構造が揃っているぶん、「答えうる問い」が薄い。優先して深掘りする件を指定してもらえれば、問いを立てて答える `ab/` を増やす。

## E. 決めてほしいこと

1. B の各項目を、報告する／しない／保留。報告する場合の窓口（Issue か、hfu が直接か）。
2. 深掘りの優先（地理・統計・OSM・テキストのどれから、`ab/` を増やすか）。
3. 横断の踏み跡を `reviewed` に上げる順序（A の 5 本から始めるか）。
