# 委託回報

下單、改單或刪單後，會收到交易所的委託或成交回報。

## 設定回呼

=== "Python"

    `stat` 為回報類型，`msg` 為回報內容。未設定回呼時，登入後會將回報印在主控台。

    ```python
    def order_callback(stat, msg):
        print(stat, msg)

    api.set_order_callback(order_callback)
    ```

    `stat` 為 `pk.constant.OrderState`。證券委託是 `OrderState.StockOrder`，證券成交是 `OrderState.StockDeal`。

=== "C#"

    ```c#
    static public void MyCallBackFunction(OrderState orderState, dynamic msg)
    {
        Console.WriteLine("my_order_callback");
        Console.WriteLine($"OrderState.{orderState} - {msg}");
    }

    pocketx.SetOrderCallback((orderState, msg) => {
        Console.WriteLine($"訂單狀態變更: {orderState} - {msg}");
    });

    ```

    ```
    [2025-10-30 14:38:43][INF][SYSTEM] Set Order Callback Successfully!!!
    ```

## 委託回報

=== "Python"

    ```python
    OrderState.StockOrder
    {
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
    ```

=== "C#"

    ```
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
                "account": "<your-account-ino>",
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

### operation

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

### order

```
id (string): 與成交回報的 trade_id 相同
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

### status

```
id (string): 與成交回報的 trade_id 相同
exchange_ts (float): 交易所時間
modified_price (float or int): 改價
cancel_quantity (int): 取消數量
order_quantity (int): 委託數量
web_id (string): 下單平台代碼
```

### contract

```
security_type (string): 商品類別
exchange (string): 交易所
code (string): 商品代碼
symbol (string): 符號
name (string): 商品名稱
currency (string): 幣別
```

## 成交回報

`stat` 為 `OrderState.StockDeal`。欄位格式與委託回報同頁的 C# 範例一併對照；目前頁面上的成交範例仍是佔位內容。
