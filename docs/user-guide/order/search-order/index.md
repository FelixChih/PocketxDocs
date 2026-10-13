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

    更新單筆後，狀態可能從 `Submitted` 變成 `PartFilled`，並帶成交明細：

    ```text
    contract=Stock(exchange=<Exchange.TSE: 'TSE'>, code='0056', symbol='TSE0056', name='元大高股息', category='0', limit_up=44.44, limit_down=36.36, update_date='20240719') order=Order(action=<Action.Buy: 'Buy'>, price=36.7, quantity=200, order_lot=<StockOrderLot.IntradayOdd: 'IntradayOdd'>, custom_field='test', price_type=<StockPriceType.LMT: 'LMT'>, order_type=<OrderType.ROD: 'ROD'>) status=OrderStatus(id='trade_test_01', status=<Status.PartFilled: 'PartFilled'>, status_code='00', order_quantity=200, deals=[Deal(seq='100095', price=36.7, quantity=100, ts=1732000639.0)], act=<Act.O: '新單'>)
    ```

    `list_trades()` 回傳當日委託清單，指定其中一筆即 `trades[0]`，內容與上面的 `Trade` 相同。

=== "C#"

    ```C#
    pocketx.UpdateStatus(account, trade);
    pocketx.ListTrades();
    ```
