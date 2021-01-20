# WebSocket API
## 1. 指令格式
```
请求格式：
{
  "op": "<value>",
  "args": ["<value1>","<value2>"]
}
```
op的取值为subscribe：订阅；unsubscribe：取消订阅；login：登录  
args: 取值为频道名，可以定义一个或者多个频道

### 1.1 响应格式：
```
正确响应格式：
{
  "data":"<data>",
  "channel":"<channel>",
  "instrumentCode":"<instrumentCode>"
}
```
```
失败响应格式：
{
  "event":"error",
  "message":"<error_message>",
  "errorCode":"<errorCode>"
}
```
## 2. Websocket api
### 2.1登陆
```
订阅指令格式：
{
  "op":"login",
  "args":["<api_key>","<passphrase>","<timestamp>","<sign>"]
}
```
```
示例：
{
  "op":"login",
  "args":[
        "985d5b66-57ce-40fb-b714-afc0b9787083",
        "123456",
        "1538054050.975",
        "7L+zFQ+CEgGu5rzCj4+BdV2/uUHGqddA9pI6ztsRRPs="
        ]
}
```
api_key：为用户申请的APIKEY  
passphrase：为申请api时所填写  
timestamp:为时间戳，是unix epoch时间，单位是秒，时间戳30秒后会过期；推荐使用time endponit 查询API 服务器的时间，如果你的服务器时间和API 服务器时间有偏差的话  
sign:为签名字符串，签名规则参照请求说明（API概述验证部分）
## 2.2 资产
```
订阅请求指令：
{
  "op":"SUBSCRIBE",
  "args":["CAPITAL:apiKey"]
}
```
其中”CAPITAL” 为通道，”apiKey” 为用户申请的APIKEY
#### 返回数据格式：
|     参数    	|     类型    	|     说明    	|
|-	|-	|-	|
|     data    	|     List    	|[<币种>,<账户余额>,<冻结金额>]    	|
|     channel    	|     String    	|     通道    	|
|     instrumentCode    	|     String    	|     币对    	|
```
返回示例：
{
  "data":["BTC","111.00111111","11.00001100"],
  "channel":"CAPITAL",”instrumentCode”:”BTC_USDT_COINBASE_ENCRY”
}
```
### 2.3 交易
```
订阅请求指令：
{
  "op":"SUBSCRIBE",
  "args":["DEAL:BTC_USDT_COINBASE_ENCRY"]
}
```
其中”DEAL”为通道，”BTC_USDT_COINBASE_ENCRY”为币对信息
#### 返回数据格式：
|     参数    	|     类型    	|     说明    	|
|-	|-	|-	|
|     data    	|     List    	|     [<交易类型>,<交易价格>,<交易数量><时间>]，交易类型 S:买入 B:卖出    	|
|     channel    	|     String    	|     通道    	|
|     instrumentCode    	|     String    	|     币对    	|
```
{
  "data":[<type>,<交易价格>,<交易数量><时间>],
  "channel":"CAPITAL"
}
```
```
返回示例：
{
    "data":[
        [
            "S",
            "8326",
            "0.2",
            1584158302636
        ],
        [
            "B",
            "8324",
            "0.1",
            1584071778560
        ]
    ],
    "channel":"DEAL",
    "instrumentCode":"BTC_USDT_COINBASE_ENCRY"
}
```
### 2.4  Ticker
```
订阅请求指令：
{
  "op":"SUBSCRIBE",
  "args":["TICKER:BTC_USDT_COINBASE_ENCRY:M1"]
}
```
其中”TICKER”为通道，”BTC_USDT_COINBASE_ENCRY” 为币对信息，”M1”为周期（详情见3. 参数说明）
#### 返回参数
|     参数    	|     类型    	|     说明    	|
|-	|-	|-	|
|     data    	|     List    	|     [编码,时间,买一,卖一,开盘价,最高价,最低价,最新价,上周期收盘价格,成交量,上周期成交量,成交量加权平均价,成交金额]    	|
|     channel    	|     String    	|     通道    	|
|     instrumentCode    	|     String    	|     币对    	|
|     period    	|     String    	|     周期    	|
```
返回示例：
{
    "data":[
        "BTC_USDT_COINBASE_ENCRY",
        1584166560000,
        "8326",
        "8351",
        "8326",
        "8326",
        "8326",
        "8326",
        "8326",
        "0",
        "0",
        "8326",
        "0"
    ],
    "channel":"TICKER",
    "instrumentCode":"BTC_USDT_COINBASE_ENCRY",
    "period":"M1"
}
```
### 2.5 Kline
```
订阅请求指令：
{
  "op":"SUBSCRIBE",
  "args":["KLINES:BTC_USDT_COINBASE_ENCRY:M1"]
}
```
其中”KLINES” 为通道，”BTC_USDT_COINBASE_ENCRY” 为币对信息，”M1”为周期（详情见3. 参数说明）
#### 返回参数
|     参数    	|     类型    	|     说明    	|
|-	|-	|-	|
|     data    	|     List    	|     [时间,开盘价,最高价,最低价,收盘价,成交数量]    	|
|     channel    	|     String    	|     通道    	|
|     instrumentCode    	|     String    	|     币对    	|
|     period    	|     String    	|     周期    	|
```
返回示例：
{
    "data":[
        [
            1584108060000,
            "8351",
            "8351",
            "8351",
            "8351",
            "0"
        ],
        [
            1584167940000,
            "8326",
            "8326",
            "8326",
            "8326",
            "0"
        ]
    ],
    "channel":"KLINES",
    "instrumentCode":"BTC_USDT_COINBASE_ENCRY",
    "period":"M1"
}
```
### 2.6 盘口
```
订阅请求指令：
{
  "op":"SUBSCRIBE",
  "args":["ORDER_BOOK:BTC_USDT_COINBASE_ENCRY:0.001"]
}
```
其中”ORDER_BOOK” 为通道，”BTC_USDT_COINBASE_ENCRY” 为币对信息，”0.001”为步长深度（调用api接口获取）
#### 返回参数
|     参数    	|     类型    	|     说明    	|
|-	|-	|-	|
|     timeStamp    	|     Long    	|     时间（毫秒）    	|
|     asks    	|     String    	|     卖盘[价格，数量，累计数量]    	|
|     bids    	|     String    	|     买盘[价格，数量，累计数量]    	|
|     channel    	|     String    	|     通道    	|
|     instrumentCode    	|     String    	|     币对    	|
```
返回示例：
{
    "data":{
        "timeStamp":1584169165556,
        "asks":[
            [
                "8999",
                "10",
                "86.897327"
            ],
            [
                "8351",
                "8.9",
                "8.9"
            ]
        ],
        "bids":[
            [
                "6249.05",
                "200",
                "4844.337605"
            ]
        ]
    },
    "channel":"ORDER_BOOK:0.001",
    "instrumentCode":"BTC_USDT_COINBASE_ENCRY"
}
```
## 3.参数说明
#### 周期参数：
| 参数 | 类型 | 说明 |
|---|---|---|
| H1 | String | 1hour |
| H4 | String | 4hour |
| H6 | String | 6hour |
| H12 | String | 12hour |
| DAY | String | 1day |
| WEEK | String | 1week |
| MONTH | String | 1month |

## 4.返回错误码
|     错误码    	|     错误内容    	|     说明    	|
|-	|-	|-	|
|     30001    	|     Invalid ACCESS_KEY    	|     无效的 access_key    	|
|     30002    	|     Invalid passphrase     	|     无效的   密钥    	|
|     30003    	|     Invalid sign    	|     无效的签名    	|
|     30004    	|     Unrecognized_request    	|     不合法的请求    	|
|     30005    	|     Channel doesn't exist    	|     通道不存在    	|
|     30006    	|     User not logged in / User must be logged   in    	|     用户没有登陆    	|