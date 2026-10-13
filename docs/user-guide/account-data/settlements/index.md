# 交割款

查詢交割款。請先登入。

=== "Python"

    未指定帳號時，查詢預設證券帳號。回傳為陣列，可轉成 DataFrame。

    ```python
    import pandas as pd

    settlements = api.settlements(api.stock_account)
    print(settlements)

    df = pd.DataFrame(item.__dict__ for item in settlements)
    print(df)
    ```

    ```text
    [Settlement(date=datetime.date(2024, 11, 14), amount=-38132.0, T=0),
     Settlement(date=datetime.date(2024, 11, 15), amount=-689690.0, T=1),
     Settlement(date=datetime.date(2024, 11, 18), amount=-111477.0, T=2)]
    ```

    以 `T` 為索引的 DataFrame：

    ```text
       date      amount
    T
    0  2024-11-14  -38132.0
    1  2024-11-15 -689690.0
    2  2024-11-18 -111477.0
    ```

=== "C#"

    ```c#
    var res = pocketx.Settlements();
    Console.WriteLine($"settlements: {res}")
    ```

    ```
    Settlements: [{"ddate":"20251030","amount":"0","tdate":0},{"ddate":"20251031","amount":"0","tdate":1},{"ddate":"20251103","amount":"175873","tdate":2}]
    ```

```
date: 交割日期
amount: 交割金額
T: T day
```

C# 回傳欄位名稱為 `ddate`、`amount`、`tdate`。
