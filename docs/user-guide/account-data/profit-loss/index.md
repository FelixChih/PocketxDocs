# 已實現損益

查詢已實現損益。請先登入，並提供帳號與日期區間。日期格式為 `YYYY-MM-DD`。

=== "Python"

    ```python
    import pandas as pd

    profit_loss = api.list_profit_loss(
        api.stock_account,
        "2024-09-04",
        "2024-11-05",
    )
    print(profit_loss)

    df = pd.DataFrame(item.__dict__ for item in profit_loss)
    print(df)
    ```

    ```text
    [StockProfitLoss(id=0, code='2845', quantity=1000, pnl=0.0, date='20241105', dseq='CA046', price=13.3, pr_ratio=0.0, seqno='463954'),
     StockProfitLoss(id=1, code='0056', quantity=24000, pnl=-59690.0, date='20241030', dseq='CA067', price=34.0, pr_ratio=-6.82, seqno='463954')]
    ```

    轉成 DataFrame 後：

    ```text
       id  code  quantity      pnl      date   dseq   price  pr_ratio    seqno
    0   0  2845      1000      0.0  20241105  CA046   13.30      0.00   463954
    1   1  0056     24000 -59690.0  20241030  CA067   34.00     -6.82   463954
    ```

=== "C#"

    ```c#
    var res = pocketx.ListProfitLoss(begin_date, end_date, pocketx.StockAccount);
    Console.WriteLine($"ProfitLoss: {res}")
    ```

    ```
    ProfitLoss: {"9802269":[{"seqno":"5540359","dseq":"CO180","price":"123","pr_ratio":"-4.06","cond":"0","id":"0","code":"4953","quantity":"2000","pnl":"-10380","date":"20251030"},{"seqno":"5540359","dseq":"CJ239","price":"115","pr_ratio":"3.24","cond":"0","id":"1","code":"3029","quantity":"1000","pnl":"3592","date":"20251009"}]}
    ```

```
seqno (string): seqno no.
dseq (string): seqno no.
price (decimal): 價格
pr_ratio (decimal): 損益比
cond (StockOrderCond): {
            Cash: 現股(預設值)
            Netting: 餘額交
            MarginTrading: 融資
            ShortSelling: 融券
            Emerging: 興櫃
        }
id: 可利用此 id 查詢明細
code: 商品代碼
quantity (int): 數量
pnl (float): 損益
date (string): 交易日期
```
