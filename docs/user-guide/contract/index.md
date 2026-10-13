# 商品檔

商品檔用於下單時指定標的。目前對外提供的商品為證券。

登入時 `fetch_contract` 預設為 `True`，會下載商品檔。若登入時設為 `False`，可再呼叫 `fetch_contracts()` 下載。

## 商品檔狀態

=== "Python"

    尚未下載時，狀態為 `FetchStatus.Unfetch`。下載完成為 `FetchStatus.Fetched`。

    ```python
    api = pk.Pocket()
    api.login(
        api_key="YOUR_API_KEY",
        password="YOUR_PASSWORD",
        fetch_contract=False,
    )
    print(api.Contracts.status)

    api.fetch_contracts(contract_download=True)
    print(api.Contracts.status)
    print(api.Contracts)
    ```

    `fetch_contract=False` 時：

    ```text
    FetchStatus.Unfetch
    ```

    手動下載完成時：

    ```text
    Spend 0:00:00.598719 !!!!!!!!!!!!!!!!!!!!!!!!
    Contracts status: Fetched
    FetchStatus.Fetched
    Indexs=() Stocks=(OES, OTC, TSE) Futures=() Options=() status=<FetchStatus.Fetched: 'Fetched'>
    ```

=== "C#"

    登入成功後會開始下載商品檔。

    ```c#
    using PocketxSDK;

    var pocketx = new Pocketx();
    var contract = pocketx.Contracts;
    Console.WriteLine(_contract);
    ```

    ```json
    {
        "Indexs":{},"Stocks":{"OTC":{"006201":{"security_type":"STK","code":"006201","symbol":"OTC006201","exchange":"OTC","limit_up":26.57,"limit_down":21.75,"reference":0.0,"margin_trading_balance":0,"short_selling_balance":0,"update_date":"2024/07/19","category":"00","day_trade":2,"name":"元大富櫃50","target_code":""}, .... }}
    }
    ```

## 查詢證券

=== "Python"

    ```python
    print(api.Contracts.Stocks.TSE)

    contract = api.Contracts.Stocks["0050"]
    contract = api.Contracts.Stocks.TSE["0050"]
    contract = api.Contracts.Stocks.TSE.TSE0050
    print(contract)
    ```

    交易所下的股票代號清單很長，下面只摘錄開頭：

    ```text
    TSE(TSE0050, TSE0051, TSE0052, TSE0053, TSE0055, TSE0056, ...)
    ```

    單一商品：

    ```text
    exchange=<Exchange.TSE: 'TSE'> code='0050' symbol='TSE0050' name='元大台灣50' category='0' limit_up=209.65 limit_down=171.55 update_date='20240719'
    ```

    `api.Contracts.Stocks.TSE["0056"]` 與 `api.Contracts.Stocks.TSE.TSE0056` 的結果相同：

    ```text
    exchange=<Exchange.TSE: 'TSE'> code='0056' symbol='TSE0056' name='元大高股息' category='0' limit_up=44.44 limit_down=36.36 update_date='20240719'
    ```

    商品欄位：

    ```
    code (str): 商品代碼
    symbol (str): 符號，例如 TSE0050
    name (str): 商品名稱
    exchange (Exchange): 交易所 {TSE, OTC, OES}
    category (str): 類別
    limit_up (float): 漲停價
    limit_down (float): 跌停價
    reference (float): 參考價
    update_date (str): 更新日期
    margin_trading_balance (int): 融資餘額
    short_selling_balance (int): 融券餘額
    day_trade (DayTrade): 可否當沖 {Yes, No, OnlyBuy}
    ```

=== "C#"

    ```c#
    var contract_0050 = _api.Contracts.Stocks["TSE"]["0050"];
    Console.WriteLine(contract_0050.ToString());
    ```

    ```json
    {
        "security_type":"STK",
        "code":"0050",
        "symbol":"TSE0050",
        "exchange":"TSE",
        "limit_up":209.65,
        "limit_down":171.55,
        "reference":0.0,
        "margin_trading_balance":0,
        "short_selling_balance":0,
        "update_date":"2024/07/19",
        "day_trade":2,
        "category":"00",
        "name":"元大台灣50",
        "target_code":"",
    }
    ```

    ```
    code (str): 商品代碼
    symbol (str): 符號
    exchange (Exchange): 交易所 {OES, OTC, TSE ...等}
    limit_up (float): 漲停價
    limit_down (float): 跌停價
    name (str): 商品名稱
    reference (float): 參考價
    margin_trading_balance (int): 融資餘額
    short_selling_balance (int): 融券餘額
    update_date (str): 更新日期
    day_trade (DayTrade): 可否當沖 {Yes, No, OnlyBuy}
    category (str): 類別
    name (str): 名稱
    ```
