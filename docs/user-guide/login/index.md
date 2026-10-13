# 登入

登入必須擁有口袋帳戶。若還沒有帳戶，可詳見 [口袋開戶](https://www.pocket.tw/openaccountonline/oa/home?mkCode=MK0000&channel=CH0003&utm_source=pocketw&openExternalBrowser=1&showYuShanBtn=Y)。

## 登入

=== "Python"

    `api_key` 是簽署文件後取得的 API 金鑰。`password` 是使用者密碼。`fetch_contract` 預設為 `True`，登入時會下載商品檔。`contracts_timeout` 預設為 `0`。

    ```python
    import pocketx as pk

    api = pk.Pocket()
    accounts = api.login(
        api_key="YOUR_API_KEY",
        password="YOUR_PASSWORD",
    )
    print(accounts)
    ```

    登入成功會回傳帳號列表，並設定預設證券帳號 `api.stock_account`、預設期貨帳號 `api.futopt_account`。

=== "C#"

    ```C#
    using PocketxSDK;

    var pocketx = new Pocketx();
    var _accounts = pocketx.Login("YOUR_API_KEY", "YOUR_SECRET_KEY");
    var flag = pocketx.ca_activate("<你的pfx路徑>", "<你的 personal_id>", "<你的 personal_id>");
    Console.WriteLine(_accounts);
    ```

    ```
    [2025-xx-xx 13:59:21][INF][SYSTEM] Welcome to Pocketx!!!
    [2025-xx-xx 13:59:21][INF][SYSTEM] Login...
    [2025-xx-xx 13:59:22][INF][SYSTEM] Connecting to PulsarService...
    [2025-xx-xx 13:59:22][INF][SYSTEM] Connected to PulsarService Successfully !!!
    ```

## 帳號

=== "Python"

    ```python
    accounts = api.list_accounts()
    print(accounts)
    print(api.stock_account)
    print(api.futopt_account)

    api.set_default_account(accounts[0])
    print(api.stock_account)
    ```

    `list_accounts()` 回傳這次登入的帳號。`stock_account` 是預設證券帳號，`futopt_account` 是預設期貨帳號。`set_default_account()` 依傳入帳號的類型，改寫對應的預設帳號。

=== "C#"

    ```c#
    using PocketxSDK;

    var pocketx = new Pocketx();
    var _accounts = pocketx.Login("YOUR_API_KEY", "YOUR_SECRET_KEY");
    Console.WriteLine($"_accounts: {_accounts}");
    ```

    ```C#
    using PocketxSDK;

    var pocketx = new Pocketx();
    var listAccounts = ListAccounts(pocketx);
    Console.WriteLine(listAccounts);
    ```

    ```
    listAccounts: [
        {"account_type":"...","person_id":"...","broker_id":"...","account_id":"...","signed":true,"username":"..."}
    ]
    ```

## 登出

=== "Python"

    ```python
    api.logout()
    ```

=== "C#"

    ```C#
    using PocketxSDK;

    var pocketx = new Pocketx();
    var res = _api.Logout();
    Console.WriteLine(res); 
    ```
