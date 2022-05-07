
# python-binance API v1.0.16


Updated 7th May 2022


This is an unofficial Python wrapper for the `Binance exchange REST API v3 <https://binance-docs.github.io/apidocs/spot/en>`_. I am in no way affiliated with Binance, use at your own risk.

This wrapper allows you to autimate binance functions.


Documentation
  https://python-binance.readthedocs.io/en/latest/

Binance API Telegram
  https://t.me/binance_api_english

Blog with examples including async
  https://sammchardy.github.io


General Features Allowed
--------

- Get Historial Exceutions
- Get Market Data Endpoints
- Execute Orders
- Get Account Details


Quick Start
-----------

`Register an account with Binance <https://accounts.binance.com/en/register?ref=10099792>`_.

`Generate an API Key <https://www.binance.com/en/my/settings/api-management>`_ and assign relevant permissions.


To use the `Spot <https://testnet.binance.vision/>`_ or `Vanilla Options <https://testnet.binanceops.com/>`_ Testnet,
pass `testnet=True` when creating the client.


.. code:: bash

    pip install python-binance


.. code:: python

    from binance import Client
    client = Client(api_key, api_secret)

    # get market depth
    depth = client.get_order_book(symbol='BNBBTC')

    # place a test market buy order, to place an actual order use the create_order function
    order = client.create_test_order(
        symbol='BNBBTC',
        side=Client.SIDE_BUY,
        type=Client.ORDER_TYPE_MARKET,
        quantity=100)

    # get all symbol prices
    prices = client.get_all_tickers()

    # withdraw 100 ETH
    # check docs for assumptions around withdrawals
    from binance.exceptions import BinanceAPIException
    try:
        result = client.withdraw(
            asset='ETH',
            address='<eth_address>',
            amount=100)
    except BinanceAPIException as e:
        print(e)
    else:
        print("Success")

    # fetch list of withdrawals
    withdraws = client.get_withdraw_history()

    # fetch list of ETH withdrawals
    eth_withdraws = client.get_withdraw_history(coin='ETH')

    # get a deposit address for BTC
    address = client.get_deposit_address(coin='BTC')

    # get historical kline data from any date range

    # fetch 1 minute klines for the last day up until now
    klines = client.get_historical_klines("BNBBTC", Client.KLINE_INTERVAL_1MINUTE, "1 day ago UTC")

    # fetch 30 minute klines for the last month of 2017
    klines = client.get_historical_klines("ETHBTC", Client.KLINE_INTERVAL_30MINUTE, "1 Dec, 2017", "1 Jan, 2018")

    # fetch weekly klines since it listed
    klines = client.get_historical_klines("NEOBTC", Client.KLINE_INTERVAL_1WEEK, "1 Jan, 2017")

Donate
------

If this repository helped you out feel free to donate.

- ETH: 0xEa04067483024C991A62332240d20D5FD94a2445

