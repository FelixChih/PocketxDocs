# 查詢狀態

請先更新委託狀態，再讀取委託。若刪單或改單失敗，請重新更新該筆委託，並確認狀態是否仍可取消或修改。

=== "Python"

    更新單筆委託，或更新指定帳號的委託後，用 `list_trades()` 取出目前委託。

    ```python
    api.update_status(trade=trade)
    print(trade)

    api.update_status(account=api.stock_account)
    trades = api.list_trades()
    print(trades)
    ```

=== "C#"

    ```C#
    pocketx.UpdateStatus(account, trade);
    pocketx.ListTrades();
    ```
