# 登入(login)

## 描述
此功能用於玩家登入，參數皆為必要參數。

## 請求 URL
{api.domain}/api/auth/login

## 請求方法
`GET`

## 請求標頭
| 標頭         | 必要 | 描述          |
|--------------|------|--------------|
| authorization | 是   | 授權令牌(ApiKey) |

## 請求參數
| 參數       | 必要 | 類型   | 描述                     |
|------------|------|--------|--------------------------|
| game       | 是   | String | 遊戲名稱，例如：`game1`   |
| platform   | 是   | String | cms代理名稱，例如：`agent`|
| username   | 是   | String | 玩家帳號，唯一值          |
| agentName  | 是   | String | 使用agent功能創建的名稱    |
<!-- | hash       | 是   | String | 參數的 SHA256 哈希值      | -->

## 請求示例
```http
GET /api/auth/login?game=game1&platform=agent HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json
```

## 成功響應
```json
{
    "code": 0,
    "success": true,
    "message": "Login success",
    "data": {
        "Url": "https: //game.91url.cc/bingo/?token=963b4744-a36e-4ec8-85db-22d141613c99\u0026username=wsky_test_agentWsky_wskyOuTest"
    }
}
```

## 失敗響應
```json
{
    "code": 9999,
    "success": false
    "error": "Username Failed"
}
```

---
# 創建代理(agent)

## 描述
此功能用於創建代理，參數皆為必要參數。

## 請求 URL
{api.domain}/api/agent

## 請求方法
`POST`

## 請求標頭
| 標頭         | 必要 | 描述          |
|--------------|------|--------------|
| authorization | 是   | 授權令牌(ApiKey) |

## 請求參數
| 參數          | 必要 | 類型   | 描述                     |
|--------------|------|--------|--------------------------|
| game         | 是   | String | 遊戲名稱，例如：`game1`   |
| platform     | 是   | String | cms代理名稱，例如：`agent` |
| agentName    | 是   | String | 使用agent功能創建的名稱     |
| merchantName | 是   | String | 商戶名，預設與`platform`相同 |
| currency     | 是   | String | 幣別                       |

## 請求示例
```http
POST /api/agent HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json

{
    "currency": "VND",
    "agentName": "agentWskyqw",
    "merchantName": "wsky_test",
    "game": "bingo",
    "platform": "wsky_test"
}
```

## 成功響應
```json
{
    "code": 0,
    "success": true,
    "message": "Successfully created",
    "data": {
        "AgentName": "agentWskyqw",
        "Currency": "VND"
    }
}
```

## 失敗響應
```json
{
    "code": 7602,
    "success": false,
    "error": "AgentName has existed."
}
```

---

# 取得代理列表(agent)

## 描述
此API用於取得遊戲中商戶身分下代理列表。

## 請求 URL
{api.domain}/api/agent

## 請求方法
`GET`

## 請求標頭
| 標頭         | 必要 | 描述          |
|--------------|------|--------------|
| authorization | 是   | 授權令牌(ApiKey) |

## 請求參數
| 參數          | 必要 | 類型   | 描述                     |
|--------------|------|--------|--------------------------|
| game         | 是   | String | 遊戲名稱，例如：`game1`   |
| platform     | 是   | String | cms代理名稱，例如：`agent` |

## 請求示例
```http
GET /api/agent?game=bingo&platform=agent HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json

```

## 成功響應
```json
{
    "code": 0,
    "success": true,
    "message": "Searching success.",
    "data": null
}
```

## 失敗響應
```json
{
    "code": 7501,
    "success": false,
    "error": "merchantNotFound"
}
```

---

# 創建玩家(createPlayer)

## 描述
此功能用於創建玩家，參數皆為必要參數。

## 請求 URL
{api.domain}/api/player/create

## 請求方法
`POST`

## 請求標頭
| 標頭         | 必要 | 描述          |
|--------------|------|--------------|
| authorization | 是   | 授權令牌(APIKEY)|

## 請求參數
| 參數          | 必要 | 類型   | 描述                     |
|--------------|------|--------|--------------------------|
| game         | 是   | String | 遊戲名稱，例如：`bingo`   |
| platform     | 是   | String | cms代理名稱，例如：`agent`|
| username     | 是   | String | 玩家名稱                 |
| agentName    | 是   | String | 使用agent功能創建的名稱    |
| currency     | 是   | String | 幣別                     |

## 請求示例
```http
POST /api/player/create HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json

{
    "currency": "VND",
    "agentName": "agentWskyqw",
    "username": "testusername",
    "game": "bingo",
    "platform": "wsky_test"
}
```

## 成功響應
```html
OK
```

## 失敗響應
```json
{
    "code": 7602,
    "success": false,
    "error": "player with name testusername already exists"
}
```

---

# 轉帳(transfer)

## 描述
此功能用於登出玩家，參數皆為必要參數。

## 請求 URL
{api.domain}/api/transaction/transfer

## 請求方法
`POST`

## 請求標頭
| 標頭          | 必要 | 描述          |
|---------------|------|---------------|
| authorization | 是    | 授權令牌(APIKEY)|

## 請求參數
| 參數           | 必要 |  類型    | 描述                       |
|---------------|------|---------|----------------------------|
| game          | 是   | String  | 遊戲名稱，例如：`bingo`        |
| platform      | 是   | String  | cms代理名稱，例如：`agent1`     |
| username      | 是   | String  | 玩家名稱                        |
| agentName     | 是   | String  | 使用agent功能創建的名稱            |
| amount        | 是   | Float64 | 轉帳金額。負數為提領，正數為存入       |
| referenceCode | 是   | String  | 轉帳參考碼。唯一值。用於後續需要查詢紀錄  |
| takeAll       | 否   | Boolean | 是否全部提領。若為 true，則 Amount 無效，會提領所有餘額|



## 請求示例
```http
POST /api/transaction/transfer HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json

{
    "agentName": "agentName",
    "username": "username",
    "game": "bingo",
    "platform": "platform",
    "amount": -1.2,
    "referenceCode": "testReferenceCode",
    "takeAll": false
}
```

## 成功響應
```json
{
    "Currency": "VND",
    "Amount": 1.2,
    "BeforeBalance": 0,
    "AfterBalance": 1.2
}
```

## 失敗響應
```json
{
    "code": 9015,
    "success": false,
    "error": "player not exist"
}
```
---

# 取得轉帳記錄(transferHistory)

## 描述
此API用於取得存提款記錄。

## 請求 URL
{api.domain}/api/transaction/history

## 請求方法
`GET`

## 請求標頭
| 標頭         | 必要 | 描述          |
|--------------|------|--------------|
| authorization | 是   | 授權令牌(ApiKey) |

## 請求參數
| 參數          | 必要 | 類型   | 描述                     |
|--------------|------|--------|--------------------------|
| game         | 是   | String | 遊戲名稱，例如：`game1`   |
| platform     | 是   | String | cms代理名稱，例如：`agent` |
| agentName    | 是   | String | 使用agent功能創建的名稱     |
| username     | 否   | String | 玩家名稱                  |
| startTime    | 否   | String | 起算時間                  |
| endTime      | 否   | String | 結算時間                  |
<!-- | referenceCode | 否   | String  | 交易流水號                  | -->
<!-- | status      | 否   | String  | 交易狀態                  | -->

## 請求示例
```http
GET /api/transaction/history?game=bingo&platform=agent&platform=agent&agentName=agent01&username=user01 HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json

```

## 成功響應
```json
{
    "code": 0,
    "success": true,
    "message": "Searching success.",
    "data": null
}
```

## 失敗響應
```json
{
    "code": 9001,
    "success": false,
    "error": "Non-owned agent"
}
```

---

# 取得遊戲記錄(gameHistory)

## 描述
此API用於取得存提款記錄。

## 請求 URL
{api.domain}/api/game/history

## 請求方法
`GET`

## 請求標頭
| 標頭         | 必要 | 描述          |
|--------------|------|--------------|
| authorization | 是   | 授權令牌(ApiKey) |

## 請求參數
| 參數          | 必要 | 類型   | 描述                     |
|--------------|------|--------|--------------------------|
| game         | 是   | String | 遊戲名稱，例如：`game1`   |
| platform     | 是   | String | cms代理名稱，例如：`agent` |
| agentName    | 是   | String | 使用agent功能創建的名稱     |
| username     | 否   | String | 玩家名稱                  |
| startTime    | 否   | String | 起算時間                  |
| endTime      | 否   | String | 結算時間                  |
<!-- | referenceCode | 否   | String  | 交易流水號                  | -->
<!-- | status      | 否   | String  | 交易狀態                  | -->

## 請求示例
```http
GET /api/game/history?game=bingo&platform=agent&platform=agent&agentName=agent01&username=user01 HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json

```

## 成功響應
```json
{
    "code": 0,
    "success": true,
    "message": "Searching success.",
    "data": null
}
```

## 失敗響應
```json
{
    "code": 9001,
    "success": false,
    "error": "Non-owned agent"
}
```

---

# 登出玩家(logout)
>其實目前這個功能沒有效果，gs那邊沒有kickout功能。

## 描述
此功能用於登出玩家，參數皆為必要參數。

## 請求 URL
{api.domain}/api/logout

## 請求方法
`POST`

## 請求標頭
| 標頭         | 必要 | 描述          |
|--------------|------|--------------|
| authorization | 是   | 授權令牌(APIKEY)|

## 請求參數
| 參數          | 必要 | 類型   | 描述                     |
|--------------|------|--------|--------------------------|
| game         | 是   | String | 遊戲名稱，例如：`game1`  |
| platform     | 是   | String | cms代理名稱，例如：`agent`|
| username     | 是   | String | 玩家名稱                |
| agentName    | 是   | String | 運營商帳號              |

## 請求示例
```http
POST /api/logout HTTP/1.1
Host: {GAME_API_URL}
Authorization: your_token
Content-Type: application/json

{
    "agentName": "agentWskyqw",
    "username": "testusername",
    "game": "bingo",
    "platform": "wsky_test"
}
```

## 成功響應
```html
OK
```

## 失敗響應
```json
{
    "code": 9015,
    "success": false,
    "error": "player not exist"
}
```
---


## 錯誤代碼列表

| 錯誤碼 | 描述                           |
|--------|--------------------------------|
| 0000   | 成功                           |
| 9999   | 失敗                           |
| 9001   | 未授權訪問                     |
| 9002   | 域名為空或過短                 |
| 9003   | 域名驗證失敗                   |
| 9004   | 加密數據為空或為零             |
| 9005   | 斷言時間戳驗證失敗             |
| 9007   | 未知操作                       |
| 9008   | 相同值                         |
| 9009   | 超時                           |
| 9010   | 讀取超時                       |
| 9011   | 重複交易                       |
| 9012   | 稍後重試                       |
| 9013   | 系統維護                       |
| 9014   | 多賬戶登錄                     |
| 9015   | 數據未找到                     |
| 9016   | 無效令牌                       |
| 9017   | 進行中                         |
| 9019   | 請求速率限制超過               |
| 9020   | 每次登錄一張遊戲票             |
| 9021   | 會話策略違規                   |
| 9022   | 遊戲維護                       |
| 9023   | 不支持的貨幣                   |
| 9024   | 贏取倍率限制                   |
| 9025   | 不支持重放                     |
| 8000   | 輸入參數錯誤                   |
| 8001   | 參數不可為空                   |
| 8002   | 參數必須為正整數               |
| 8003   | 不允許負數參數                 |
| 8005   | 日期秒數格式錯誤               |
| 8006   | 未達到時間要求                 |
| 8007   | 僅允許數字參數                 |
| 8008   | 參數未找到                     |
| 8009   | 時間間隔超過                   |
| 8010   | 參數過長                       |
| 8013   | 日期分鐘格式錯誤               |
| 7001   | 父ID未找到                     |
| 7002   | 父帳戶被暫停                   |
| 7003   | 父帳戶被鎖定                   |
| 7004   | 父帳戶已關閉                   |
| 7405   | 已登出                         |
| 7501   | 用戶ID未找到                   |
| 7502   | 用戶被暫停                     |
| 7503   | 用戶被鎖定                     |
| 7504   | 用戶已關閉                     |
| 7505   | 用戶未在遊戲中                 |
| 7601   | 無效的用戶ID                   |
| 7602   | 帳戶已存在                     |
| 7603   | 無效的用戶名                   |
| 7604   | 密碼要求                       |
| 7605   | 無效的操作碼                   |
| 6001   | 現金餘額不足                   |
| 6002   | 用戶餘額為零                   |
| 6003   | 不允許負提款                   |
| 6004   | 重複轉賬                       |
| 6005   | 重複的流水號                   |
| 6006   | 現金餘額不足警告               |
| 6009   | 存款限額超過                   |
| 6010   | 餘額限額超過                   |
| 6011   | 信用限額超過                   |
| 6101   | 不允許取消                     |
| 6901   | 用戶正在遊戲中                 |
