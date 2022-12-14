## Client Credentials Grant Flow

Client Credentials Grant Flow は、ユーザの手続きなくリソースサーバに問い合わせするための認証フローです。

本プロジェクトはマイクロサービスアーキテクチャを採用しており、各サービスを OAuth クライアントとして実装します。

### OAuth クライアントの作成

まず、IAM から OAuth クライアントを手動で作成します。

!!! 発行した認証情報は厳重に管理してください

### アクセストークンの取得

IAM で作成した OAuth クライアントを使って、アクセストークンを取得します。

```sh
curl -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Authorization: Basic {クライアントID}:{クライアントシークレット}をBase64でエンコードした文字列" \
  -X POST "https://{domain}/oauth2/token" \
  -d "grant_type=client_credentials"
```

認証に成功すると、以下のようなレスポンスを得られます。

```json
{
  "access_token": "eyJraWQiOiI0MGUxMGI5Yy1kZDMyLTQ1OTctYjc1Mi04YTRhZmJjNTQxYjAiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjbGllbnQxIiwiYXVkIjoiY2xpZW50MSIsIm5iZiI6MTY2Njg2MDY2MCwic2NvcGUiOlsibWUiLCJ1c2VyIl0sImlzcyI6Imh0dHA6XC9cL2xvY2FsaG9zdDo4MDgwIiwiZXhwIjoxNjY2ODYxNTYwLCJpYXQiOjE2NjY4NjA2NjB9.IrPxmwT0SAc6NQmeVQ4XeLehQIqz45jQbiBzEY6NMpmJgdoFhQOlIbgiIlJMTxfqhaGqf0IHy3D9rGx45QrAsLlXVPelQHJiELS3QEJ_SSdFDWsGNWMNBMaCxXhuwjr_xq-7idHJHjndCTatiK8eeIXrOlRP5-N3gQBGXCDRjQZR1O6x1LZM1p6ZjFMWNi3Xzh8Dfhp_IdPLBecuyx50mFprAuFhN66ClBsCE4H0emeZuaOEQTUAXGbtUwIrWUsFmMeuSCSRsmZPoDGRQ5RWuf4XXf8R4M4TTB3RUxxuGIjiS04bBpTYoXlt6Ppyn9mJa_z61FszYKWwlfxoZGr1Jg",
  "scope": "me user",
  "token_type": "Bearer",
  "expires_in": 900
}
```

## リソースサーバへのアクセス

認可サーバである IAM から発行されたアクセストークンを使うと、リソースサーバへの問い合わせが可能になります。

問い合わせ時は、Authorization ヘッダーに先ほど得られたアクセストークンを指定してください。

```
Authorization: Bearer {アクセストークン}
```

## スコープ

| スコープ  | 概要                                             |
| --------- | ------------------------------------------------ |
| user:read | ユーザリスト、もしくは個別の情報を取得できます。 |
| email     | ユーザに向けてメールを送信できます。             |

## SSO について

現時点は IAM を SSO プロバイダとして提供する予定はありません。

IAM のユーザデータを利用したい場合は、Membership Console の一機能としてリリースすることを検討してください。
