# 委託回報內容

回報的接收方式見 [委託回報](../../../callback/index.md)。以下是證券委託回報的欄位。

=== "Python"

    `set_order_callback` 的第一個參數是 `stat`，第二個參數 `msg` 是下面這個物件。證券委託的 `stat` 為 `OrderState.StockOrder`。

    ```python
    {
        "operation": {
            "op_type": "Cancel",
            "op_code": "",
            "op_msg": ""
        },
        "order": {
            "action": "Buy",
            "price": "56.0",
            "quantity": "5",
            "order_type": "ROD",
            "price_type": "LMT",
            "order_cond": "Cash",
            "order_lot": "Common",
            "custom_field": "Test"
        },
        "status": {
            "modified_price": "56.0",
            "cancel_quantity": "1000",
            "order_quantity": "0"
        },
        "contract": {
            "security_type": "STK",
            "exchange": "TSE",
            "code": "0050",
            "symbol": "TSE0050",
            "name": "元大台灣50",
            "currency": "TWD"
        }
    }
    ```

=== "C#"

    ```C#
    OrderState.StockOrder - {
        "stat": "SORDER",
        "msg": {
            "operation": {
                "op_type": "Cancel",
                "op_code": "",
                "op_msg": ""
            },
            "order": {
                "id": "",
                "seqno": 355251,
                "ordno": "CP354",
                "account": "<your-account-info>",
                "action": "Buy",
                "price": "56.0",
                "quantity": "5",
                "order_type": "ROD",
                "price_type": "LMT",
                "order_cond": "Cash",
                "order_lot": "Common",
                "custom_field": "Test"
            },
            "status": {
                "id": "",
                "exchange_ts": "113842123",
                "modified_price": "56.0",
                "cancel_quantity": "1000",
                "order_quantity": "0",
                "web_id": ""
            },
            "contract": {
                "security_type": "STK",
                "exchange": "TSE",
                "code": "0050",
                "symbol": "TSE0050",
                "name": "元大台灣50",
                "currency": "TWD"
            }
        }
    }
    ```

## 欄位

**operation**

```
op_type (string): {
        "New": 新單, 
        "Cancel": 刪單,  
        "UpdatePrice": 改價, 
        "UpdateQty": 改量
    }
op_code (string): {"00": 成功, others: 失敗}
op_msg (string): 錯誤訊息
```

**order**

```
id (string): 與成交回報的trade_id相同
seqno (string): 平台單號
ordno (string): 委託單號
account (dict): 帳號資訊
action (string): 買賣別 {Buy, Sell}
price (float or int): 委託價格
quantity (int): 委託數量
order_type (string): 委託類別 {ROD, IOC, FOK}
price_type (string): {LMT: 限價, MKT: 市價, MKP: 範圍市價}
order_cond (string): {
            Cash: 現股, 
            MarginTrading: 融資, 
            ShortSelling: 融券
        }
order_lot (string): {
            Common: 整股, 
            Fixing: 定盤, 
            Odd: 盤後零股, 
            IntradayOdd: 盤中零股
        }
custom_field (string): 自訂欄位
```

**status**

```
id (string): 與成交回報的trade_id相同
exchange_ts (float): 交易所時間
modified_price (float or int): 改價
cancel_quantity (int): 取消數量
order_quantity (int): 委託數量
web_id (string): 下單平台代碼
```

**contract**

```
security_type (string): 商品類別
exchange (string): 交易所
code (string): 商品代碼
symbol (string): 符號
name (string): 商品名稱
currency (string): 幣別
```

## 成交回報

```
...
```
