# 證券

下單前，請先登入並激活憑證。

## 激活憑證

=== "Python"

    ```python
    api.activate_ca(
        ca_path=r"D:\TWCA\YOUR_PERSON_ID.pfx",
        ca_passwd="YOUR_CA_PASSWORD",
        person_id="YOUR_PERSON_ID",
    )
    ```

    成功時會印出憑證生效日與到期日。

=== "C#"

    激活憑證的寫法見 [登入](../../login/index.md) 範例中的 `ca_activate`。

## 委託單

=== "Python"

    ```
    price (float or int): 價格
    quantity (int): 委託數量。整股為張數，零股為股數
    action (pk.constant.Action): {Buy: 買, Sell: 賣}
    price_type (pk.constant.StockPriceType): {LMT: 限價, MKT: 市價, FLT: 平盤, LMU: 漲停, LMD: 跌停}
    order_type (pk.constant.OrderType): {ROD, IOC, FOK}
    order_lot (pk.constant.StockOrderLot): {Common: 整股, Fixing: 定盤, Odd: 盤後零股, IntradayOdd: 盤中零股, BlockTrade: 鉅額}
    order_cond (pk.constant.StockOrderCond): 預設 Cash（現股）
    daytrade_short (bool): 預設 False
    account (Account): 下單帳號。未帶入時，證券單使用 api.stock_account
    custom_field (str): 備註
    ```

=== "C#"

    ```
    price (float or int): 價格
    quantity (int): 委託數量
    action (Action): {Buy: 買, Sell: 賣}
    price_type (StockPriceType): {LMT: 限價, MKT: 市價, MKP: 範圍市價}
    order_type (OrderType): 委託類別 {ROD, IOC, FOK}
    order_cond (StockOrderCond): {Cash:現股, MarginTrading:融資, ShortSelling:融券}(目前只支持Cash)
    order_lot (StockOrderLot): {Common:整股, Fixing:定盤, Odd:盤後零股, IntradayOdd:盤中零股}
    daytrade_short (DayTradeShort): 現沖 {Yes, No}
    account (:obj:Account): 下單帳號  
    custom_field (string): 備註
    ca (binary): the ca of this order
    ```

## 下單

下單時請提供商品檔與委託單。

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
    var contract = pocketx.Contracts.Stocks["TSE"]["0050"];
    ```

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

    ```C#
        {
        "contract":{
            "security_type":"STK",
            "code":"0050",
            "symbol":"TSE0050",
            "exchange":"TSE",
            "limit_up":70.8,
            "limit_down":58.0,
            "reference":0.0,
            "margin_trading_balance":0,
            "short_selling_balance":0,
            "update_date":"2025/10/31",
            "category":"00",
            "day_trade":"2",
            "name":"元大台灣50",
            "target_code":""
        },
        "order":{
            "action":"Buy",
            "price":60.0,
            "quantity":3,
            "price_type":"LMT",
            "order_type":"ROD",
            "order_lot":"Common",
            "order_cond":"Cash",
            "daytrade_short":0,
            "id":"",
            "seqno":"484614",
            "ordno":"CL561",
            "account":"<your-account_msg>",
            "custom_field":"Test",
            "ca":"..."
        },
        "status":{
            "id":"",
            "status":"Submitted",
            "status_code":"00",
            "order_datetime":"20251031100509",
            "msg":"已處理 9802243 的 0050，價格為 60.0，數量為 3 (整張)",
            "modified_ts":0.0,
            "modified_price":0.0,
            "order_quantity":3000,
            "cancel_quantity":0,
            "act":0,
            "deals":null
        }
    }
    ```

## 改價

零股不得改價。

=== "Python"

    ```python
    trade = api.update_order(trade=trade, price=61)
    print(trade)
    ```

=== "C#"

    ```C#
    var updatedTrade = pocketx.UpdateOrder(trade, price: 51.0, quantity: 0);
    ```

    ```json
    {
        "contract":{
            "security_type":"STK",
            "code":"0050",
            "symbol":"TSE0050",
            "exchange":"TSE",
            "limit_up":70.8,
            "limit_down":58.0,
            "reference":0.0,
            "margin_trading_balance":0,
            "short_selling_balance":0,
            "update_date":"2025/10/31",
            "category":"00",
            "day_trade":"2",
            "name":"元大台灣50",
            "target_code":""
        },
        "order":{
            "action":"Buy",
            "price":60.0,
            "quantity":3,
            "price_type":"LMT",
            "order_type":"ROD",
            "order_lot":"Common",
            "order_cond":"Cash",
            "daytrade_short":"",
            "id":"",
            "seqno":"484614",
            "ordno":"CL561",
            "account":"<your-account-info>",
            "custom_field":"Test",
            "ca":"..."
            },
        "status":{
            "id":"",
            "status":"Submitted",
            "status_code":"00",
            "order_datetime":"20251031100509",
            "msg":"已處理 9802243 的 0050，價格為 60.0，數量為 3 (整張)",
            "modified_ts":0.0,
            "modified_price":0.0,
            "order_quantity":3000,
            "cancel_quantity":0,
            "act":0,
            "deals":null
        }
    }
    ```

## 改量

改量只能減少原委託單的委託數量。

=== "Python"

    ```python
    trade = api.update_order(trade=trade, qty=1)
    print(trade)
    ```

=== "C#"

    ```C#
    var updatedTrade2 = pocketx.UpdateOrder(trade, price: 0, quantity: 2);
    ```

## 刪單

=== "Python"

    ```python
    trade = api.cancel_order(trade=trade)
    print(trade)
    ```

=== "C#"

    ```C#
    var updatedTrade2 = pocketx.UpdateOrder(trade, price: 0, quantity: 2);
    ```
