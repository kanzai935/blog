## WebSocketまとめ

### インプット
- [ハイパフォーマンス ブラウザネットワーキング
――ネットワークアプリケーションのためのパフォーマンス最適化](https://www.oreilly.co.jp/books/9784873116761/)
  - 17章　WebSocket
- Amazon API Gateway 開発者ガイド
  - [WebSocket API の操作](https://docs.aws.amazon.com/ja_jp/apigateway/latest/developerguide/apigateway-websocket-api.html)

### アウトプット
- 1つの TCP 接続でサーバーとクライアントがやり取りする
- WebSocket の接続リクエストは HTTP リクエストのプロトコルを WebSocket にアップグレードさせたもの
- リクエストの `Sec-WebSocket-Key` に署名をつけたレスポンス `Sec-WebSocket-Accept` を返す
  - 接続リクエスト
  ```
  GET /resource HTTP/1.1
  Host: example.com
  Upgrade: websocket
  Connection: upgrade
  Sec-WebSocket-Version: 13
  Sec-WebSocket-Key: E4WSEcseoWr4csPLS2QJHA==
  ```
  - 接続レスポンス
  ```
  HTTP/1.1 101 OK
  Upgrade: websocket
  Connection: upgrade
  Sec-WebSocket-Accept: 7eQChgCtQMnVILefJAO6dK5JwPc=
  ```
- テキストメッセージとバイナリを送受信できる
- 重いメッセージは分割して送信が推奨される
- 送信中は他のメッセージは送信できないのでリクエスト送信の優先度に注意
- TLSで保護されたWSSの使用を推奨
