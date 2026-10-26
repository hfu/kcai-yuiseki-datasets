# kcai-un-docs の最初のプロンプト（クラウドエージェント向けの叩き台）

hfu が `dwg7/kcai-un-docs` を作ったあと、別のクラウドエージェントに渡すための最初のプロンプト。作成: 2026-10-26（`hfu/kcai-yuiseki-datasets` のセッション）。以下の `---` の間を、そのまま渡せる。

---

あなたは `dwg7/kcai-un-docs` の作業担当のエージェントです。日本語で作業し、敬語は不要です。

## このリポジトリは何か

[kcai](https://github.com/dwg7/kcai)（Knowledge Co-created with AI、AI と共創した知識）の方式で、**国連の総会と安保理の文書（yuiseki/un-docs）を一次資料とする、踏み跡**（verified case を出典と照らして確かめた短い Markdown）を残すインスタンスです。kcai は AI の名前ではなく、BYOA（各自が自分の AI を使う）のための知識表現です。先行するインスタンスに `dwg7/kcai-terrio`（terrio で遊んだ記録）と `dwg7/kcai-survey-training` があります。管理責任者は hfu（外部への発信、承認、マージの権限）です。

kcai がうまく回るかは、**よい問いをシードできるか**にかかっている、というのが hfu の見立てで、このリポジトリはそれを試す場です。つまり目的は、国連文書の要約を作ることではなく、**問いごとに、どう確かめたか、どこまで確かめられたか、どこが外れやすいか**を残すことです。

## 最初に読むもの（この順）

1. `dwg7/kcai` の `README.md`、`PRINCIPLES.md`、`AGENTS.md`、`docs/knowledge-format.md`、`docs/instance.md`、`docs/asking.md`、`docs/human-role.md`、`docs/distribution.md`、`templates/instance/`
2. `dwg7/kcai-terrio` の `AGENTS.md`、`DECISIONS.md`、`knowledge/README.md`（先行インスタンスの運用の例。`verified_how`、`stale`、`plays/` の使い方）
3. `hfu/kcai-yuiseki-datasets`（ブランチ `claude/youthful-goldberg-tq7dzs`）の次のファイル。アクセスできなければ hfu に質問する:
   - `knowledge/cross/un-docs-kcai-feasibility.md`（un-docs の実測、試した問い、始め方の案）
   - `knowledge/cross/un-docs-geospatial-institutions.md` と `checks/un-docs-geospatial-institutions.tsv`（分類済みの226文書）
   - `knowledge/datasets/un-docs.md`、`knowledge/cross/text-corpora.md`
   - `checks/check-2026-10-26-un-docs-geospatial.md`（検索の手順）

## 作業の進め方

テンプレート（`dwg7/kcai` の `templates/instance/`）を使って足場を作り、`AGENTS.md`、`DECISIONS.md`、`SOURCES.md`、`QUESTIONS.md`（種の問いの台帳）を置く。形式と検査（`scripts/validate_knowledge.py` など）は kcai に従う。食い違いは `DECISIONS.md` に書く（消さない）。

### 段階 0：下準備（1本）

un-docs の読み方の踏み跡（`knowledge/un-docs-reading-guide.md` など）を書く。材料はすべて `hfu/kcai-yuiseki-datasets` に実測済みである（再確認して構わない）:

- 39,363 行のうち本文が異なるのは 36,835。
- 安保理決議 S/RES は 4,248 行だが番号は 2,699 通り（1〜2699）。`S/RES/1 (1946)` と `S/RES/1(1946)` のような綴り違いで二重に入っている。**記号は空白を除いて正規化する。**
- S/RES は 2699（2023-10-02）まで。2700〜2722 は無い。S/PV は範囲内で 90 欠け。
- 総会決議の合冊（`A/NN/49(Vol.I)` など）は、個別の決議と同じ本文を持つ。**語の検索では除く。**
- OCR は 1,864 行（`text_source = ocr`）。1980 年代の約 20%、1990 年代の約 13%。古い年代の語の検索は取りこぼしがある。
- 日付が取れない行が 996。`date_distributed`・`date_adopted`・`date_other` は別の事実。
- 総会（A/RES、A/PV など）と安保理（S/RES、S/PV、S/PRST、S/ 数字の文書）の**英語**に限られる。ECOSOC、専門機関、委員会、各ミッションの予算文書は無い。

データの読み方（pin した版）:

```python
import duckdb
u = 'https://huggingface.co/datasets/yuiseki/un-docs/resolve/6cd1cf0/documents.parquet'  # 409MB。列は id, lang, body, text_source, pdf, date_*, n_chars
con = duckdb.connect(); con.execute('install httpfs; load httpfs')
rows = con.execute(f"select id, coalesce(date_adopted, date_distributed, date_other), text_source, md5(body), body from read_parquet('{u}') where regexp_matches(body, '(?i)geo-?spatial')").fetchall()
```

（`pip install duckdb`。`pkill -f` のようにコマンドラインで自分のシェルまで巻き込むものを使わない。）

### 段階 1：種の問い（3本）

1. **「国連の文書で地理空間情報という言葉はいつ頃から使われ始め、どのような課題に関連して、どのような枠組みで議論され、どのような結論が得られているか。どのような地理的傾向を持つか。」** `hfu/kcai-yuiseki-datasets` に初回の試行がある（`geospatial` の初出は A/RES/61/111、2006-12-14 など）。**語の展開**（geospatial、geographic information、GIS、remote sensing、earth observation、geodetic、mapping、satellite imagery）、重複の除去、範囲の明示、面ごと（初出、課題、枠組み、結論、地理）の確かめた度合いを、踏み跡として整える。地理的傾向は未集計なので、国名の出現や S/PV の発言国の集計を試す。国連は国を「語る」文書であって、地図上の位置を示す文書ではない点に注意。
2. **「保護する責任（responsibility to protect）の概念としての初出は？」** 既知の答えがある落とし穴の見本。素朴な番号順の先頭は S/RES/1393（2002、通常の用法）で、概念としての初出は S/RES/1674（2006）と A/RES/60/1。この外れ方と、同じ概念とみなす条件の決め方を残す。
3. **UN Geospatial Information Section、ブリンディジの国連兵站基地（UNLB）／グローバル・サービスセンターの地理空間・情報・通信技術サービス、各平和維持活動ミッションの GIS 機能に関する表現の悉皆的な把握。** 初回の分類が `checks/un-docs-geospatial-institutions.tsv` にある（226 文書）。ここから、(a) 検索語の漏れの検討（`mapping`、`imagery`、`SAGE`、`UNOSAT` など。いずれも un-docs に別途ある）、(b) 分類の確かめ直し（特に『その他（自動）』54 文書と M-ミッション 25 文書）、(c) 名称と組織の年表の確定、(d) 公式サイトの原文との照合、を行い、踏み跡にする。**ミッションの GIS 機能の本体は予算文書にあり un-docs に無い**ので、そこは未確認のまま書く。

踏み跡は小さく（1主題1ファイル）、`status: draft` で出す。

## 書き方の約束

- 出典は**文書記号**（例 `S/RES/1674 (2006)`、`A/RES/69/308`）と、公式サイトの文書（`https://docs.un.org/en/<記号>`）。un-docs の抽出テキストは二次的な写しなので、**引用する箇所は可能なら公式の原文と照らす**。公式サイトに届かない場合は、届かないと書き（制限をすり抜けない）、hfu に一覧で伝える。
- 本文の転載はしない。要約と該当箇所の指示にとどめる。引用が必要なら短く（一文以内）。
- **確かめた度合いを正直に書く**: 実際に un-docs を検索して確かめたこと、公式の原文で確かめたこと、読んだだけのこと、未確認のこと。推測を埋めない。
- 範囲を一文で言う（「un-docs＝総会と安保理の英語文書、安保理決議は 2699 まで」）。「国連が○○を議論してきた」と一般化しない。
- 検索語、試して外れた語、外れ方（多義、重複、OCR、合冊）を踏み跡に残す。同義語・関連語の表は次の問いに再利用できる。
- AI は `reviewed` 以上にしない。人（hfu）が確認して `reviewed_by` に記録する。
- 国連の立場、国境、地図、紛争に関わる主題は、文書の記述を引くにとどめ、評価を足さない。公開できる内容に限定し、敬意をもって書く。

## 守ること

- 外部（国連、Hugging Face、GitHub の他のリポジトリ）への投稿・コメント・PR はしない。発信は hfu が行う。
- 認証情報を扱わない。公開データだけを使う。大きなデータ（un-docs の 409MB など）をリポジトリに入れない。一時ファイルはリポジトリ外に置く。
- 通信先の制限をすり抜けない。届かない配信先は hfu に一覧で伝える。
- 判断が分かれることは推測で埋めず、hfu に質問する。決定は `DECISIONS.md` に追記する。
- コミットは小さく、指定されたブランチに。PR は、hfu が求めたときだけ作る。

## 最初の報告に含めること

- 作った足場と、`kcai` との食い違い（あれば）。
- 段階 0 の踏み跡の要点と、確かめられなかったこと。
- 段階 1 の3問それぞれについて、進み具合、確かめた度合い、次に必要な一次資料。
- hfu への質問（未確定の点）。

---

## 追補（2026-10-26、引き継ぎ時に別途メッセージで送った内容）

起動後、親セッション側の un-docs に関する残りの作業を、次の7項目として kcai-un-docs 側のセッションに引き継いだ（優先度つき）: (1) 公式原文との照合（12 文書記号）、(2) 『その他（自動）』54 文書と『M-ミッション』25 文書の分類の確かめ直し、(3) 語の展開の検討（imagery 174、mapping 37、UNOSAT 15、geo-information 58 の粗い数値つき）、(4) 地理的傾向の集計、(5) 種の問いの候補（安保理の衛星画像、S/PV の採決記録、宇宙空間決議の定型文の追跡）、(6) 下準備の宿題（S/RES/2700〜2722、S/PV 欠番 90、A/RES/2777〜2779(XXVI)、綴りの重複と正規化）、(7) 上流への報告候補の下書き（投稿はしない）。取り込む資料のコミットは 1b0f565。
