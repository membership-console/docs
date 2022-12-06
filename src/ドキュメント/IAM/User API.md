## ユーザリスト取得 API

### URI

```
GET
/api/oauth2/users
```

### レスポンスボディ

```json
{
  "users": [
    {
      "id": 0,
      "firstName": "string",
      "lastName": "string",
      "email": "string",
      "entranceYear": 0,
      "roles": ["IAM_ADMIN"],
      "userGroups": [
        {
          "id": 0,
          "name": "string",
          "roles": [0]
        }
      ]
    }
  ]
}
```

## ユーザ取得 API

### URI

```
GET
/api/oauth2/users/{user_id}
```

### レスポンスボディ

```json
{
  "id": 0,
  "firstName": "string",
  "lastName": "string",
  "email": "string",
  "entranceYear": 0,
  "roles": ["IAM_ADMIN"],
  "userGroups": [
    {
      "id": 0,
      "name": "string",
      "roles": [0]
    }
  ]
}
```
