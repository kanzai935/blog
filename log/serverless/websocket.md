# WebSocketまとめ

## インプット
- [ハイパフォーマンス ブラウザネットワーキング
――ネットワークアプリケーションのためのパフォーマンス最適化](https://www.oreilly.co.jp/books/9784873116761/)
  - 17章　WebSocket
- RFC6455
  - [The WebSocket Protocol](https://tools.ietf.org/html/rfc6455)
- Amazon API Gateway 開発者ガイド
  - [WebSocket API の操作](https://docs.aws.amazon.com/ja_jp/apigateway/latest/developerguide/apigateway-websocket-api.html)

## アウトプット
### 基本仕様
- 1つの TCP 接続でサーバーとクライアントがやり取りする
- WebSocket の接続リクエストは HTTP リクエストのプロトコルを WebSocket にアップグレードさせたもの
- リクエストの `Sec-WebSocket-Key` に署名をつけたレスポンス `Sec-WebSocket-Accept` を返す
- クライアントからサブプロトコル `Sec-WebSocket-Protocol` のリストを渡され、サポートするサブプロトコルを返す
- 接続リクエスト
```
GET /resource HTTP/1.1
Host: example.com
Upgrade: websocket
Connection: upgrade
Sec-WebSocket-Version: 13
Sec-WebSocket-Key: E4WSEcseoWr4csPLS2QJHA==
Sec-WebSocket-Extensions: deflate-frame
Sec-WebSocket-Protocol: soap, wamp
```
- 接続レスポンス
```
HTTP/1.1 101 OK
Upgrade: websocket
Connection: upgrade
Sec-WebSocket-Accept: 7eQChgCtQMnVILefJAO6dK5JwPc=
Sec-WebSocket-Extensions: deflate-frame
Sec-WebSocket-Protocol: soap
```
- テキストメッセージとバイナリを送受信できる
- 重いメッセージは分割して送信が推奨される
- 送信中は他のメッセージは送信できないのでリクエスト送信の優先度に注意
- TLSで保護されたWSSの使用を推奨

### API Gateway
- 次の4つのルートを使用
  - `$connect` ルート
    - WebSocket API 間の永続的な接続が開始された時のルート
  - `$disconnect` ルート
    - クライアントまたはサーバーが API から切断した時のルート
  - カスタムルート
    - 一致するルートが見つかった時、メッセージに対してルート選択式が評価された時のルート
    - ルート選択式例
      - `$request.body.action`
    - `$joinroom` ルートを呼び出すメッセージ例
      - `{"action":"joinroom","roomname":"developers"}`
  - `$default` ルート
    - ルート選択式をメッセージに対して評価できない場合や、一致するルートが見つからない時のルート
- メッセージペイロードは128kBまでで、最大フレームサイズは32KBなので、それより大きい場合は分割すること
