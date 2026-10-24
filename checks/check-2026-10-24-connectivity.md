# 配信先の到達性チェック（2026-10-24）

## 結果

- `huggingface.co` : 到達不能（DNS 解決失敗）
- `e-stat.go.jp` : 到達不能（DNS 解決失敗）
- `github.com` : 到達可能

## 実行した確認

```bash
python - <<'PY'
import socket
for host in ['huggingface.co','e-stat.go.jp','github.com']:
    try:
        socket.getaddrinfo(host, 443)
        print(f'{host}: DNS OK')
    except Exception as e:
        print(f'{host}: DNS FAIL {e}')
PY
```

## 判断

この環境からは Hugging Face と e-Stat に到達できないため、制限をすり抜けようとせず、GitHub 上で公開されている Yuiseki さんの踏み跡を使って作業を進める。必要なら、藤村に許可リスト追加候補として `huggingface.co` と `e-stat.go.jp` を伝える。
