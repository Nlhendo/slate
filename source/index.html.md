---
title: Atmos API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://atmosbot.com/auth/sign-up'>Sign Up for an Atmos API Key</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Atmos API! You can use our API to access cryptocurrency OHLCV candle data from Binance & Kraken. This data can be utilised and itegrated into your custom application.

We have language bindings in Curl, JavaScript, Python, and C#! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

Here's a simple guide to walk you through generating Atmos API keys. 

Alternatively you can register for an API key at our [portal](http://api.atmosbot.com/api).


# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('personalatmosapikey')
```

```python
import kittn

api = kittn.authorize('personalatmosapikey')
```

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.atmosbot.com/v1/<exchange>/pairs" \
  -H "x-atmos-key: personalatmosapikey"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('personalatmosapikey');
```

> Make sure to replace `personalatmosapikey` with your API key.

You can authenticate API keys to allow access the cryptocurrency candle data. 

Atmos Authentication is header-based, and requires one parameter x-atmos-key:
Your personalised API key is required for all API requests to the server in a header that looks like the following:

`x-atmos-key: personalatmosapikey`

<aside class="notice">
You must replace <code>personalatmosapikey</code> with your personal API key.
</aside>



# Rate Limiting

Atmos API requests are capped at 20 requests per minute. Exceeding this threshold will result in the return of a 429 response code.


# Candle Data

## Get All Pairs

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('personalatmosapikey')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('personalatmosapikey')
api.kittens.get()
```

```shell
curl "http://api.atmosbot.com/v1/<exchange>/pairs" \
  -H "x-atmos-key: personalatmosapikey"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('personalatmosapikey');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  
    "AAVEAUD",
    "AAVEETH",
    "AAVEEUR",
    "AAVEGBP",
    "AAVEUSD",
    "AAVEXBT",
    "ADAAUD",
    "ADAETH",
    "ADAEUR",
    "ADAGBP",
    "ADAUSD",
    "ADAUSDT",


]
```

This endpoint retrieves all crypto currency pairings from a given exchange.

### HTTP Request

`GET http://api.atmosbot.com/v1/<exchange>/pairs/`

### Query Parameters

Parameter | Description
---------  | -----------
`<exchange>` | must be changed to supported exchange of your choice `kraken` or `binance`.


<aside class="notice">
Remember — You need to add your Atmos API key to the header!
</aside>

## Specific Pair OHLCV

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://api.atmosbot.com/v1/<exchange>/symbol/ohlcv" \
  -H "x-atmos-key: personalatmosapikey"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
    "results": [{
        "id": "607ec20c2972f20011a150d9",
        "symbol": "ETHUSDT",
        "startTime": "2021-04-20T12:00:00.000Z",
        "ticks": [{
            "time": "2021-04-20T12:00:00.000Z",
            "open": "2193.87000",
            "high": "2193.87000",
            "low": "2193.87000",
            "close": "2193.87000",
            "baseVolume": "5.03426978",
            "trades": 4
        }, {
            "time": "2021-04-20T12:01:00.000Z",
            "open": "2191.10000",
            "high": "2191.93000",
            "low": "2190.55000",
            "close": "2190.55000",
            "baseVolume": "5.36900000",
            "trades": 4
```

This endpoint retrieves a specific pair. 

<aside class="warning">Replace <code>&lt;exchange&gt;</code> with the exchange of your choice.</aside>

### HTTP Request

`GET http://api.atmosbot.com/v1/<exchange>/symbol/ohlcv`

###  Limit Parameters

`GET http://api.atmosbot.com/v1/<exchange>/ETHUSDT/ohlcv/?limit=2`

Parameter | Description
--------- | -----------
limit | limits the number of returned candle buckets

###  Page Parameters

`GET http://api.atmosbot.com/v1/<exchange>/ETHUSDT/ohlcv/?page=5`

Parameter | Description
--------- | -----------
Page | Allows you to view the candles from a specific page. The first element (page) will be 0.


###  Start time Parameters

Utilising iso 8601 formating which can be described as follows: YYYY-MM-DDTHH:mm:ss. sssZ 

The timezone is always UTC as denoted by the suffix "Z

`GET http://api.atmosbot.com/v1/<exchange>/ETHUSDT/ohlcv/?start_time=2021-04-09T10:20:00.000Z`

Parameter | Description
--------- | -----------
start_time | sets start time of candle ticks

###  End time Parameters

Utilising iso 8601 formating which can be described as follows: YYYY-MM-DDTHH:mm:ss. sssZ 

The timezone is always UTC as denoted by the suffix "Z

`GET http://api.atmosbot.com/v1/<exchange>/ETHUSDT/ohlcv/?end_time=2021-04-09T10:50:00.000Z`

Parameter | Description
--------- | -----------
end_time | sets end time of candle ticks


### Chaining Parameters

All of the aformentioned parameters can be combined, composing of a series of field-value pairs.

Example:

`GET http://api.atmosbot.com/v1/<exchange>/ETHUSDT/ohlcv/?end_time=2021-04-09T10:50:00.000Z&page=0`

> The request returns JSON structured like this:

```json
{
    "results": [{
        "id": "60702a4549522600129b5046",
        "symbol": "ETHUSDT",
        "startTime": "2021-04-09T10:20:00.000Z",
        "ticks": [{
            "time": "2021-04-09T10:20:00.000Z",
            "open": "2099.37000",
            "high": "2099.37000",
            "low": "2099.37000",
            "close": "2099.37000",
            "baseVolume": "0.26256048",
            "trades": 1
        }, {
            "time": "2021-04-09T10:22:00.000Z",
            "open": "2098.43000",
            "high": "2098.43000",
            "low": "2098.43000",
            "close": "2098.43000",
            "baseVolume": "2.00000000",
            "trades": 1
        }, {
            "time": "2021-04-09T10:23:00.000Z",
            "open": "2098.00000",
            "high": "2098.00000",
            "low": "2098.00000",
            "close": "2098.00000",
            "baseVolume": "0.48935249",
            "trades": 2
        }]
```

## Pair Latest 

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://api.atmosbot.com/v1/<exchange>/symbol/ohlcv/latest" \
  -H "Authorization: personalatmosapikey"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
    "result": {
        "time": "2021-04-20T11:39:00.000Z",
        "open": "2178.21000",
        "high": "2178.74000",
        "low": "2178.21000",
        "close": "2178.74000",
        "baseVolume": "13.37782288",
        "trades": 7
    }
```

This endpoint returns the latest candle tick for a specific crypto currency pairing.

### HTTP Request

`GET http://api.atmosbot.com/v1/<exchange>/symbol/ohlcv/latest`



