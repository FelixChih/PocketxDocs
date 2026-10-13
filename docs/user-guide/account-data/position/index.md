# 未實現損益

查詢未實現損益（庫存）。請先登入。

=== "Python"

    未指定帳號時，查詢預設證券帳號。回傳為陣列，可轉成 DataFrame。

    ```python
    import pandas as pd

    positions = api.list_positions()
    print(positions)

    df = pd.DataFrame(item.__dict__ for item in positions)
    print(df)
    ```

=== "C#"

    ```c#
    var res = pocketx.ListPositions(pocketx.StockAccount);
    Console.WriteLine($"Positions: {res}")
    ```

    ```json
    Positions: [
        {
            "yd_quantity": 20000,
            "cond": 0,
            "margin_purchase_amount": 0,
            "collateral": 0,
            "short_sale_margin": 0,
            "interest": 0,
            "id": 0,
            "code": "2337",
            "direction": "Buy",
            "quantity": 22000,
            "price": 25.79,
            "last_price": 34.65,
            "pnl": 192212.0
        },
        {
            "yd_quantity": 2000,
            "cond": 0,
            "margin_purchase_amount": 0,
            "collateral": 0,
            "short_sale_margin": 0,
            "interest": 0,
            "id": 1,
            "code": "4953",
            "direction": "Sell",
            "quantity": 0,
            "price": 0.0,
            "last_price": 122.5,
            "pnl": 0.0
        }
    ]
    ```

```
yd_quantity (int): 昨日庫存數量
cond (StockOrderCond): {
        Cash: 現股(預設值), 
        Netting: 餘額交割,
        MarginTrading: 融資, 
        ShortSelling: 融券, 
        Emerging: 興櫃
    }
margin_purchase_amount (int):  融資金額
collateral (int): 擔保品
short_sale_margin (int): 保證金
interest (int): 除息
id (int): 部位代碼
code (str):商品代碼
direction (str): {Buy: 買, Sell: 賣}
quantity (int): 數量
price (float): 平均價格
last_price (float): 目前股價
pnl (float): 損益
```
