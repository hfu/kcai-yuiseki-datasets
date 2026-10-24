# terrio での yuiseki-datasets の読み取り確認（2026-10-24）

環境: Claude Code クラウドセッション、Linux x86_64、PyPI の terrio 0.4.2（`terrio --version` は `terrio 0.4.2`）。データは estat-boundary-2020 のコミット 823195c（香川 r2ka37、東京 r2ka13 の Parquet、香川の Shapefile zip）。一時ファイルはスクラッチに置き、リポジトリには入れていない。

## 実行した確認

```sh
terrio info r2ka37.parquet                  # Geometry: None, CRS: unknown, geometry: Blob
terrio convert r2ka37.parquet out.geojson   # 1,010 地物、geometry は全て null
TERRIO_HTTP_LOG=YES terrio info https://huggingface.co/datasets/yuiseki/estat-boundary-2020/resolve/823195c/parquet/r2ka37.parquet
                                            # 64KiB Range(206) の後、全体 GET 4,520,782 バイト
terrio info r2ka37.shp                      # Polygon, EPSG:4612, 1,010（参考の 1 回のみ。hfu の判断で追試しない）
terrio convert r2ka37.shp out.geojson       # 幾何は Polygon、属性は文字化け
terrio info jp-admin-2026-09 municipalities.parquet            # MultiPolygon, 1918, EPSG:4612（HEAD e6c87b1）
terrio convert municipalities.parquet j37.geojson --where "pref_code = '37'"   # 17 地物、日本語属性は正しい
```

jp-admin は HEAD の sha e6c87b1、abr-src は 3677b24、geo-triples-jp-gov は df079b5 のファイル。duckdb（pip）で `parquet_kv_metadata` と `parquet_metadata` から `geo` キーと行グループ数を読んだ。

## 判断

- 結果は knowledge/cross/terrio-usage-possibilities.md の「確かめたこと」に反映した。
- terrio の挙動に見える点（Parquet の BLOB を幾何と見ない、cp932 を読めない）は、上流への報告候補だが、投稿は hfu が行う。このリポジトリからは行わない。

# estat-boundary-2020-duplicate-boundaries の実データ照合（同日）

duckdb で r2ka13（東京、6,021 行）と r2ka37（香川、1,010 行）を数えた。e-Stat 定義書（A002005212020.pdf、同日取得）の記述と一致:

- 人口の合計は、KIGO_E が空か E1 の行だけで全体の合計と一致（東京 14,047,594、香川 950,244）。En（n≧2）の行は人口 0。
- E1 を持つ KEY_CODE のうち、E1 の行と M の行が別になるもの: 東京 16/119、香川 4/51。
- AREA_MAX_F が NULL の行で人口が 0 より大きいもの: 東京 15/419、香川 4/106。
- 例外: 東京の KEY_CODE が 2 桁（`13`）の行は、E の重複でなく別の理由で同じキーが繰り返される（人口 0）。M が複数ある KEY_CODE は東京に 1 件（この `13`）。

2 県だけの確認で、全国の数は未確認。
