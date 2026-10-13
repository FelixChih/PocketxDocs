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
