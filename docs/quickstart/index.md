# 快速開始

下單前請先登入，並激活憑證。

## 登入並激活憑證

=== "Python"

    ```python
    import pocketx as pk

    api = pk.Pocket()
    accounts = api.login(
        api_key="YOUR_API_KEY",
        password="YOUR_PASSWORD",
    )
    api.activate_ca(
        ca_path=r"D:\TWCA\YOUR_PERSON_ID.pfx",
        ca_passwd="YOUR_CA_PASSWORD",
        person_id="YOUR_PERSON_ID",
    )
    print(accounts)
    ```

    ```text
    =========================================== User Logged in ===========================================
    Spend 0:00:00.598719 !!!!!!!!!!!!!!!!!!!!!!!!
    Contracts status: Fetched

    簽章憑證 生效日：
    20241107104927

    簽章憑證 到期日：
    20241121235959

    [StockAccount(person_id='YOUR_PERSON_ID', broker_id='6620', account_id='YOUR_STOCK_ACCOUNT_ID', signed=True, username='USERNAME', nanoid='YOUR_NANOID')]
    ```

=== "C#"

    ```C#
    using PocketxSDK;

    var pocketx = new Pocketx();
    var _accounts = pocketx.Login("YOUR_API_KEY", "YOUR_SECRET_KEY");
    var flag = pocketx.ca_activate("<你的pfx路徑>", "<你的 personal_id>", "<你的 personal_id>");
    Console.WriteLine(_accounts);
    ```

## 下單

=== "Python"

    ```python
    contract = api.Contracts.Stocks["0050"]
    order = api.Order(
        price=60,
        quantity=1,
        action=pk.constant.Action.Buy,
        price_type=pk.constant.StockPriceType.LMT,
        order_type=pk.constant.OrderType.ROD,
        order_lot=pk.constant.StockOrderLot.Common,
        custom_field="test",
        account=api.stock_account,
    )
    trade = api.place_order(contract, order)
    print(trade)
    ```

    ```text
    status=OrderStatus(id='trade_test_01', status=<Status.Submitted: 'Submitted'>, status_code='00', msg='已處理 YOUR_ACCOUNT_ID 的 0056，價格為 36.8，數量為 2（整張）', order_quantity=2, act=<Act.O: '新單'>)
    ```

    完整 `Trade` 與改價、改量、刪單的回傳見 [證券下單](../user-guide/order/stock/index.md)。

=== "C#"

    ```C#
    var order = new StockOrder()
    {
        price = <price>,
        quantity = <qty>,
        action = Action.Buy,
        price_type = StockPriceType.LMT,
        order_type = OrderType.ROD,
        order_lot = orderLot,
        daytrade_short = DayTradeShort.No,
        custom_field = "Test",
    };
    var trade = pocketx.PlaceOrder(contract, order);
    ```
