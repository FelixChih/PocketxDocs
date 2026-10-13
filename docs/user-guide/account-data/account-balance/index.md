# 銀行餘額

查詢證券交割帳戶餘額。請先登入。

=== "Python"

    ```python
    balance = api.account_balance()
    print(balance)
    ```

    ```text
    AccountBalance(status=<FetchStatus.Fetched: 'Fetched'> acc_balance=4108825.0 date='2024-11-14T02:47:52.006281' errmsg='')
    ```

    未指定帳號時，查詢預設證券帳號 `api.stock_account`。

=== "C#"

    ```c#
    var res = pocketx.AccountBalance();
    Console.WriteLine($"accountBalance: {res}");
    ```

    ```
    accountBalance: accountBalance: {"acc_balance":0.0,"date":"xx/xx/2025 05:59:26","errmsg":""}
    ```

```
acc_balance (float): 餘額
date (str): 查詢日期
errmsg (str): 錯誤訊息
```
