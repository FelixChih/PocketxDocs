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
