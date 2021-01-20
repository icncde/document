# CFD
## 1、委托下单
### 1.1 接口说明
描述： 差价交易提供的限价单和市价单委托下单接口。  
Url： /openapi/cfd/v1/entrust  
请求方式：POST  
是否是私有接口：是
### 1.2 参数
#### 1.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|code|String|Y|交易产品编码|
|command|String|Y|方向：”B”：买多、”S”：卖空|
|type|String|Y|订单类型:”MARKET”:市价、”LIMIT”：限价|
|level|Int|Y|杠杆倍数|
|currency|String|Y|币种|
|qty|String|Y|数量|
|price|String|N|价格|
|stopLossPrice|String|N|止损价|
|stopGainPrice|String|N|止盈价|
### 1.3示例
#### 1.3.1 请求示例
>请求path:  /openapi/cfd/v1/entrust
```
请求json:
{
    "code": "BTC_USD_COINBASE_CFD_BTC",
     "command": "B",
     "type": "LIMIT",
     "lever": 50,
     "currency": "BTC",
     "qty": 1,
     "price": "2000",
     "stopLossPrice": "1963",
     "stopGainPrice": "2000.05"
}
```
#### 1.3.2 返回示例
```
{
    "orderId": 1061096037664423936,
     "result": true
}
```
## 2、批量委托下单
### 2.1 接口说明
描述： 差价交易提供的限价单和市价单批量委托下单接口。  
Url： /openapi/cfd/v1/entrust/batch  
请求方式：POST  
是否是私有接口：是
#### 2.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|code|String|Y|交易产品编码|
|command|String|Y|方向：”B”：买多、”S”：卖空|
|type|String|Y|订单类型:”MARKET”:市价、”LIMIT”：限价|
|level|Int|Y|杠杆倍数|
|currency|String|Y|币种|
|qty|Double|Y|数量|
|price|String|N|价格|
|stopLossPrice|String|N|止损价|
|stopGainPrice|String|N|止盈价|
### 2.3 示例
#### 2.3.1 请求示例
>请求path:  /openapi/cfd/v1/entrust/batch
```
请求 json:
[{
    "code": "BTC_USD_COINBASE_CFD_BTC",
    "command": "B",
    "type": "MARKET",
    "lever": 50,
    "currency": "BTC",
    "qty": 1
}, {
    "code": "BTC_USD_COINBASE_CFD_BTC",
    "command": "B",
    "type": "MARKET",
    "lever": 50,
    "currency": "BTC",
    "qty": 1
}]
```
#### 2.3.2 返回示例
```
[{
    "orderId": 1061098681053216768,
    "result": true
}, {
    "orderId": 1061098681279709184,
    "result": true
}]
```
## 3、修改委托单
### 3.1接口说明
描述： 差价交易对委托中订单进行修改的接口。  
Url： /openapi/cfd/v1/entrust/update  
请求方式：POST  
是否是私有接口：是
#### 3.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|orderId|String|Y|订单id|
|stopLossPrice|String|N|止损价|
|stopGainPrice|Int|N|止盈价|
|amount|String|N|追加保证金金额|
### 3.3 示例
#### 3.3.1 请求示例
>请求path:  /openapi/cfd/v1/entrust/update
```
请求 json:
{
    "orderId": 1061096037664423936,
    "amount": 1.111,
    "stopLossPrice": 23,
    "stopGainPrice": 2000.04
}
```
#### 3.3.2 返回示例
```
{
  "orderId":1061096037664423936,
  "result":true
}
```
## 4、撤单
### 4.1接口说明
描述： 差价交易对委托中订单进行撤单操作接口。  
Url： /openapi/cfd/v1/cancel  
请求方式：POST  
是否是私有接口：是
### 4.2 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|orderId|String|Y|订单id|
### 4.3 返回示例
```
{
  "orderId":1061096037664423936,
  "result":true
}
```
## 5、批量撤单
### 5.1接口说明
描述： 差价交易对委托中订单进行批量撤单操作的接口。  
Url： /openapi/cfd/v1/cancel/batch  
请求方式：POST  
是否是私有接口：是
#### 5.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|orderId|String|Y|订单ID|
### 5.3示例
#### 5.3.1 请求示例
> 请求path:  /openapi/cfd/v1/cancel/batch
```
请求 json:
[1058827173536362496,1058827173536362496]
```
#### 5.3.2 返回示例
```
[{
    "errorMessage": "订单不存在",
    "orderId": "1058827173536362496",
    "result": false
}, {
    "errorMessage": "订单不存在",
    "orderId": "1058827173536362496",
    "result": false
}]
```
## 6、持仓单列表
### 6.1接口说明
描述： 查询差价账户持仓单列表接口。  
Url： /openapi/cfd/v1/deal  
请求方式：GET  
是否是私有接口：是
#### 6.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|currency|String|N|币种|
|pageNo|Int|Y|当前页|
|pageSize|Int|Y|每页条数|
#### 6.2.2 返回参数
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|rows|List|当页数据|
|pageNo|Int|当前页|
|pageSize|Int|每页条数|
|totalPage|Int|总页数|
|totalRow|Int|总条数|
Rows参数：
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|code|String|金融产品code|
|commodity|String|商品code|
|name|String|商品名称|
|currency|String|币种|
|lever|Int|杠杆倍数|
|side|Int|方向:1:买多，2：卖空|
|type|Int|类型:1:市价、2：限价|
|status|Int|委托单状态：1：委托、2：成交、3：取消、4：手动平仓、5：爆仓、6：止盈平仓、7：止损平仓|
|entrustTime|Long|委托时间|
|dealTime|Long|成交时间|
|qty|String	数量|
|avgPrice|String|成交价|
|closePrice|String|平仓价|
|stopLossPrice|String|止损价|
|stopGainPrice|String|止盈价|
|entrustPrice|String|委托价|
|brokePrice|String|爆仓价|
|Margin|String|占用保证金|
|Scale|String|合约乘数|
|openFee|String|开仓佣金手续费|
|closeFee|String|平仓佣金|
|overNightFee|String|隔夜费用|
|profitLoss|String|盈亏|
|profitLossRatio|String|盈亏百分比|
|createdOn|String|创建时间|
#### 6.3.1 返回示例
```
{
        "avgPrice": 11408.57000000000000000000,
        "brokePrice": 11197.51000000000000000000,
        "code": "BTC_USD_COINBASE_CFD_BTC",
        "commodity": "BTC",
        "createdOn": 1597308343000,
        "currency": "BTC",
        "dealTime": 1597308345000,
        "entrustPrice": 11408.57000000000000000000,
        "entrustTime": 1597308345000,
        "id": "1061098681279709184",
        "lever": 50,
        "margin": 0.00022817140000000000,
        "openFee": 0.00000570428500000000,
        "overNightFee": 0E-20,
        "profitLoss": 0.00031160,
        "qty": 1.00000000000000000000,
        "scale": 0.00000100000000000000,
        "side": 0,
        "status": 2,
        "type": 1
}
```

## 7、持仓单详情
### 7.1接口说明
描述： 查询差价账户持仓单详情接口。  
Url： /openapi/cfd/v1/deal/{orderId}  
请求方式：GET  
是否是私有接口：是
#### 7.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|orderId|String|Y|订单id|
#### 7.2.2 返回参数
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|code|String|金融产品code|
|commodity|String|商品code|
|name|String|商品名称|
|currency|String|币种|
|lever|Int|杠杆倍数|
|side|Int|方向:1:买多，2：卖空|
|type|Int|类型:1:市价、2：限价|
|status|Int|委托单状态：1：委托、2：成交、3：取消、4：手动平仓、5：爆仓、6：止盈平仓、7：止损平仓|
|entrustTime|Long|委托时间|
|dealTime|Long|成交时间|
|qty|String|数量|
|avgPrice|String|成交价|
|closePrice|String|平仓价|
|stopLossPrice|String|止损价|
|stopGainPrice|String|止盈价|
|entrustPrice|String|委托价|
|brokePrice|String|爆仓价|
|Margin|String|占用保证金|
|Scale|String|合约乘数|
|openFee|String|开仓佣金手续费|
|closeFee|String|平仓佣金|
|overNightFee|String|隔夜费用|
|profitLoss|String|盈亏|
|profitLossRatio|String|盈亏百分比|
|createdOn|String|创建时间|
#### 7.3.1 返回示例
```
{
    "avgPrice": 11408.57000000000000000000,
        "brokePrice": 11197.51000000000000000000,
        "code": "BTC_USD_COINBASE_CFD_BTC",
        "commodity": "BTC",
        "createdOn": 1597308343000,
        "currency": "BTC",
        "dealTime": 1597308345000,
        "entrustPrice": 11408.57000000000000000000,
        "entrustTime": 1597308345000,
        "id": "1061098681279709184",
        "lever": 50,
        "margin": 0.00022817140000000000,
        "openFee": 0.00000570428500000000,
        "overNightFee": 0E-20,
        "profitLoss": 0.00031160,
        "qty": 1.00000000000000000000,
        "scale": 0.00000100000000000000,
        "side": 0,
        "status": 2,
        "type": 1
}
```
## 8、持仓单修改
### 8.1接口说明
描述： 差价交易对持仓单进行追加保证金、止盈止损修改接口。  
Url： /openapi/cfd/v1/deal/update  
请求方式：POST  
是否是私有接口：是
### 8.2 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|orderId|Long|Y|订单id|
|amount|String|N|追保金额|
|stopLossPrice|String|N|止损价格|
|stopGainPrice|String|N|止盈价格|
### 8.3示例
#### 8.3.1 请求示例
>请求path:  /openapi/cfd/v1/deal/update
```
请求 json:
{
    "orderId": 1061096037664423936,
    "amount": 1.111,
    "stopLossPrice": 23,
    "stopGainPrice": 2000.04
}
```
#### 8.3.2 返回示例
```
{
  "orderId":1061096037664423936,
  "result":true
}
```
## 9、平仓
### 9.1接口说明
描述： 差价交易对持仓单进行平仓操作。  
Url： /openapi/cfd/v1/close/{orderId}  
请求方式：POST  
是否是私有接口：是
### 9.2 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|orderId|Long|Y|订单id|
#### 9.3.2 返回示例
```
{
  "orderId":1061096037664423936,
  "result":true
}
```
## 10、委托单详情
### 10.1接口说明
描述： 查询差价账户持仓单详情接口。  
Url： /openapi/cfd/v1/entrust/{orderId}  
请求方式：GET  
是否是私有接口：是
#### 10.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|orderId|String|Y|订单id|
#### 10.2.2 返回参数
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|code|String|金融产品code|
|commodity|String|商品code|
|name|String|商品名称|
|currency|String|币种|
|lever|Int|杠杆倍数|
|side|Int|方向:1:买多，2：卖空|
|type|Int|类型:1:市价、2：限价|
|status|Int|委托单状态：1：委托、2：成交、3：取消、4：手动平仓、5：爆仓、6：止盈平仓、7：止损平仓|
|entrustTime|Long|委托时间|
|dealTime|Long|成交时间|
|qty|String|数量|
|avgPrice|String|成交价|
|closePrice|String|平仓价|
|stopLossPrice|String|止损价|
|stopGainPrice|String|止盈价|
|entrustPrice|String|委托价|
|brokePrice|String|爆仓价|
|Margin|String|占用保证金|
|Scale|String|合约乘数|
|openFee|String|开仓佣金手续费|
|closeFee|String|平仓佣金|
|overNightFee|String|隔夜费用|
|profitLoss|String|盈亏|
|profitLossRatio|String|盈亏百分比|
|createdOn|String|创建时间|
#### 10.3.1 返回示例
```
{
    "code": "BTC_USD_COINBASE_CFD_BTC",
    "commodity": "BTC",
    "createdOn": 1597224730000,
    "currency": "BTC",
    "entrustPrice": 121.00000000000000000000,
    "entrustTime": 1597224732000,
    "id": "1060747982665969664",
    "lever": 50,
    "margin": 2.22200242000000000000,
    "qty": 1.00000000000000000000,
    "scale": 0.00000100000000000000,
    "side": 0,
    "status": 1,
    "stopGainPrice": 121.05000000000000000000,
    "stopLossPrice": 23.00000000000000000000,
    "type": 0
}
```
## 11、委托单列表
### 11.1接口说明
描述： 查询差价账户委托单列表接口。  
Url： /openapi/cfd/v1/entrust  
请求方式：GET  
是否是私有接口：是
#### 11.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|currency|String|N|币种|
|pageNo|Int|Y|当前页|
|pageSize|Int|Y|每页条数|
#### 11.2.2 返回参数
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|rows|List|当页数据|
|pageNo|Int|当前页|
|pageSize|Int|每页条数|
|totalPage|Int|总页数|
|totalRow|Int|总条数|
Rows参数：
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|code|String|金融产品code|
|commodity|String|商品code|
|name|String|商品名称|
|currency|String|币种|
|lever|Int|杠杆倍数|
|side|Int|方向:1:买多，2：卖空|
|type|Int|类型:1:市价、2：限价|
|status|Int|委托单状态：1：委托、2：成交、3：取消、4：手动平仓、5：爆仓、6：止盈平仓、7：止损平仓|
|entrustTime|Long|委托时间|
|dealTime|Long|成交时间|
|qty|String|数量|
|avgPrice|String|成交价|
|closePrice|String|平仓价|
|stopLossPrice|String|止损价|
|stopGainPrice|String|止盈价|
|entrustPrice|String|委托价|
|brokePrice|String|爆仓价|
|Margin|String|占用保证金|
|Scale|String|合约乘数|
|openFee|String|开仓佣金手续费|
|closeFee|String|平仓佣金|
|overNightFee|String|隔夜费用|
|profitLoss|String|盈亏|
|profitLossRatio|String|盈亏百分比|
|createdOn|String|创建时间|
#### 11.3.1 返回示例
```
{
    "pageNo": 1,
    "pageSize": 10,
    "rows": [{
    "code": "BTC_USD_COINBASE_CFD_BTC",
            "commodity": "BTC",
            "createdOn": 1597224730000,
            "currency": "BTC",
            "entrustPrice": 121.00000000000000000000,
            "entrustTime": 1597224732000,
            "id": "1060747982665969664",
            "lever": 50,
            "margin": 2.22200242000000000000,
            "name": "BTC/USD",
            "qty": 1.00000000000000000000,
            "scale": 0.00000100000000000000,
            "side": 0,
            "status": 1,
            "stopGainPrice": 121.05000000000000000000,
            "stopLossPrice": 23.00000000000000000000,
            "type": 0
}],
    "totalPage": 1,
    "totalRow": 4
}
```
## 12、历史订单列表
### 12.1接口说明
描述： 查询差价历史订单列表接口。  
Url： /openapi/cfd/v1/order/his  
请求方式：GET  
是否是私有接口：是
#### 12.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|currency|String|Y|币种|
|status|Int|N||
|pageNo|Int|Y|当前页|
|pageSize|Int|Y|每页条数|
#### 12.2.2 返回参数
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|rows|List|当页数据|
|pageNo|Int|当前页|
|pageSize|Int|每页条数|
|totalPage|Int|总页数|
|totalRow|Int|总条数|
Rows参数：
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|code|String|金融产品code|
|commodity|String|商品code|
|name|String|商品名称|
|currency|String|币种|
|lever|Int|杠杆倍数|
|side|Int|方向:1:买多，2：卖空|
|type|Int|类型:1:市价、2：限价|
|status|Int|委托单状态：1：委托、2：成交、3：取消、4：手动平仓、5：爆仓、6：止盈平仓、7：止损平仓|
|entrustTime|Long|委托时间|
|dealTime|Long|成交时间|
|qty|String|数量|
|avgPrice|String|成交价|
|closePrice|String|平仓价|
|stopLossPrice|String|止损价|
|stopGainPrice|String|止盈价|
|entrustPrice|String|委托价|
|brokePrice|String|爆仓价|
|Margin|String|占用保证金|
|Scale|String|合约乘数|
|openFee|String|开仓佣金手续费|
|closeFee|String|平仓佣金|
|overNightFee|String|隔夜费用|
|profitLoss|String|盈亏|
|profitLossRatio|String|盈亏百分比|
|createdOn|String|创建时间|
#### 12.3.1 返回示例
```
{
    "pageNo": 1,
    "pageSize": 10,
    "rows": [{
    "code": "BTC_USD_COINBASE_CFD_BTC",
            "commodity": "BTC",
            "createdOn": 1597312910000,
            "currency": "BTC",
            "entrustPrice": 2000.00000000000000000000,
            "entrustTime": 1597307715000,
            "id": "1061096037664423936",
            "lever": 50,
            "margin": 1.11104000000000000000,
            "name": "BTC/USD",
            "qty": 1.00000000000000000000,
            "scale": 0.00000100000000000000,
            "side": 0,
            "status": 3,
            "stopGainPrice": 2000.05000000000000000000,
            "stopLossPrice": 23.00000000000000000000,
            "type": 0
}],
    "totalPage": 1,
    "totalRow": 4
}
```
## 13、资产列表
### 13.1接口说明
描述： 查询差价账户个人资产列表接口。  
Url： /openapi/cfd/v1/assets  
请求方式：GET  
是否是私有接口：是
#### 13.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|currency|String|N|币种|
#### 13.2.2 返回参数
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|currency|String|币种|
|balance|String|可用|
|freeze|String|冻结|
|tradeLock|String|可转锁仓|
|transferLock|Int|可交易锁仓|
|totalAssets|Int|总资产|
|profitLoss|Int|未实现盈亏|
|ratio|String|资金占比|
#### 13.3.1 返回示例
```
[{
    "balance": 997.7777,
    "currency": "BTC",
    "freeze": 2.2224,
    "profitLoss": 0.0006,
    "totalAssets": 1000.0007,
    "tradeLock": 0.0000,
    "transferLock": 0.0000
}, {
    "balance": 10000.0000,
    "currency": "USDT",
    "freeze": 0.0000,
     "profitLoss": 0.0000,
     "totalAssets": 10000.0000,
     "tradeLock": 0.0000,
     "transferLock": 0.0000
}]
```
## 14、账单列表
### 14.1接口说明
描述： 查询差价账户账单列表接口。  
Url： /openapi/cfd/v1/waters  
请求方式：POST  
是否是私有接口：是
#### 14.2.1 请求参数
|参数|类型|必填|说明|
| -------------|:--------------:|:--------------:|:--------------:|
|cause|In|N|转账类型 (全选传空)；12005-交易解冻，12006-平仓，12003-交易冻结，12004-追加保证金冻结，12002-其他账户转币到此账户，12001-转币到其他账户|
|currency|String|N	币种|
|days|Int|Y|前推日期|
|pageNo|Int|Y|当前页|
|pageSize|Int|Y|每页条数|
#### 14.2.2 返回参数
|参数|类型|描述|
| -------------|:--------------:|:--------------:|
|Id|Long|流水id|
|cause|Int|转账类型|
|causeName|String|转账类型名称|
|createdOn|long|创建时间|
|currency|String|币种|
|amount|String|发生金额|
#### 14.3.1 返回示例
```
{
    "pageNo": 1,
    "pageSize": 10,
    "rows": [{
    	  "amount": 1.11104,
            "cause": 12005,
            "causeName": "12005",
            "createdOn": 1597312910000,
            "currency": "BTC",
            "id": 1060990894744215559
}, {
    	  "amount": 0.00004,
            "cause": 12004,
            "causeName": "12004",
            "createdOn": 1597311904000,
            "currency": "BTC",
            "id": 1060990894744215558
}],
   "totalPage": 2,
   "totalRow": 20
}
```