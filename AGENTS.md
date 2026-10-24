# AGENTS.md

このリポジトリは、Yuiseki さんが公開しているデータセット群と、その使い方を記録した `docs/datasets/` を読み、データセットが答えうる問いと全体像の踏み跡を残す試行です。

## 方針

- 公開可能な内容に限定し、敬意をもって記す。
- すべての文書は、一次資料と Yuiseki さんのファイルを指して書く。引き写しはしない。
- 未確認の点は「未確認」と書き、推測を埋めない。
- 踏み跡は Markdown で残し、AI 自体は共有しない。
- 形式は `id` / `title` / `status` / `sources` / `authors` / `reviewed_by` / `updated` / `related` を持つ `---` フロントマターを基本とし、本文は `## 要点` から `## 出典` で閉じる。

## 置き場所

- `knowledge/datasets/`: データセットごとの問答の踏み跡
- `knowledge/cross/`: データセット群の見取り図やカテゴリ、スタイル、パターン、実務
- `ab/`: 効き目の確かめ
- `checks/`: 確かめた記録
- `DECISIONS.md`: 決めたことと理由

## ルール

- `sources` には、一次資料と Yuiseki さんの該当ファイルを記す。
- `verified_how` は `read-data` / `read-card` / `read-docs` のいずれかを使う。
- `pattern` は `questions` / `landscape` / `categories` / `styles` / `pattern` / `practice` / `re-walk` / `ab-test` のいずれかを使う。
- 重要な仮説や判定は、出典のある言い回しに限定する。
