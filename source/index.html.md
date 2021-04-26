---
title: Atmos API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - c: C#
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

We have language bindings in cURL, JavaScript, Python, and C#! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

Here's a simple guide to walk you through generating Atmos API keys. 

Alternatively you can register for an API key at our [portal](https://api.atmosbot.com/api).


# Authentication



```c

```

```python

```

```javascript


```



You can authenticate API keys to allow access the cryptocurrency candle data. 

Atmos Authentication is header-based, and requires one parameter x-atmos-key:
Your personalised API key is required for all API requests to the server in a header that looks like the following:

`x-atmos-key: youratmosapikey`

<aside class="notice">
You must replace <code>youratmosapikey</code> with your personal API key.
</aside>



# Rate Limiting

Atmos API requests are capped at 20 requests per minute. Exceeding this threshold will result in the return of a 429 response code.


# Candle Data

## Get All Pairs

```c
var client = new RestClient("https://api.atmosbot.com/v1/<exchange>/pairs/");
client.Timeout = -1;
var request = new RestRequest(Method.GET);
request.AddHeader("x-atmos-key", "youratmosapikey");
request.AddHeader("", "

");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```python
import http.client

conn = http.client.HTTPSConnection("api.atmosbot.com")
payload = ''
headers = {
  'x-atmos-key': 'youratmosapikey',
  '': '

'
}
conn.request("GET", "/v1/binance/pairs/", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.atmosbot.com/v1/<exchange>/pairs" \
  -H "x-atmos-key: youratmosapikey"
```


```javascript
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function() {
  if(this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.atmosbot.com/v1/<exchange>/pairs/");
xhr.setRequestHeader("x-atmos-key", "youratmosapikey");
xhr.setRequestHeader("", "\n\n");

xhr.send();
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

`<exchange>` | must be changed to supported exchange of your choice `kraken` , `binance` or `coinbase`.

### Query Parameters

Parameter | Type  | Required  |  Description
---------  | ----------- | ---------  | ----------- | 
`<exchange>`    |   Striing | Yes | must be changed to supported exchange of your choice `kraken` , `binance` or `coinbase`.



<aside class="notice">
Remember — You need to add your Atmos API key to the header!
</aside>

## Specific Pair OHLCV

```c
var client = new RestClient("https://api.atmosbot.com/v1/<exchange>/<symbol>/ohlcv");
client.Timeout = -1;
var request = new RestRequest(Method.GET);
request.AddHeader("x-atmos-key", "youratmosapikey");
request.AddHeader("", "

");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```python
import http.client

conn = http.client.HTTPSConnection("api.atmosbot.com")
payload = ''
headers = {
  'x-atmos-key': 'youratmosapikey',
  '': '

'
}
conn.request("GET", "/v1/<exchange>/<symbol>/ohlcv", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl "http://api.atmosbot.com/v1/<exchange>/<symbol>/ohlcv" \
  -H "x-atmos-key: youratmosapikey"
```

```javascript
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function() {
  if(this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.atmosbot.com/v1/<exchange>/<symbol>/ohlcv");
xhr.setRequestHeader("x-atmos-key", "youratmosapikey");
xhr.setRequestHeader("", "\n\n");

xhr.send();
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
<aside class="warning">Replace <code>&lt;symbol&gt;</code> with the crypto pairing of your choice e.g. BTCUSDT .</aside>

### HTTP Request

`GET /v1/<exchange>/<symbol>/ohlcv`


###  Parameters

Parameter | Type  | Required  |  Description
---------  | ----------- | ---------  | ----------- | 
limit | String | Optional | Limits the number of returned candle buckets
page | String | Optional | Allows you to view the candles from a specific page. The first parameter value will be 0.
start_time | String | Optional | sets start time of candle ticks ..Format ISO 8601  YYYY-MM-DDTHH:mm:ss. sssZ 
end_time |  String | Optional | sets end time of candle ticks ..Format ISO 8601  YYYY-MM-DDTHH:mm:ss. sssZ 

###  Limit Parameters

`GET v1/<exchange>/<symbol>/ohlcv/?limit=2`



`GET /v1/<exchange>/<symbol>/ohlcv/?page=5`



`GET /v1/<exchange>/<symbol>/ohlcv/?start_time=2021-04-09T10:20:00.000Z`



`GET /v1/<exchange>/<symbol>/ohlcv/?end_time=2021-04-09T10:50:00.000Z`




### Chaining Parameters

All of the aformentioned parameters can be combined, composing of a series of field-value pairs.

Example:

`GET v1/<exchange>/<symbol>/ohlcv/?end_time=2021-04-09T10:50:00.000Z&page=0`

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

```c
var client = new RestClient("https://api.atmosbot.com/v1/<exchange>/<symbol>/ohlcv/latest");
client.Timeout = -1;
var request = new RestRequest(Method.GET);
request.AddHeader("x-atmos-key", "youratmosapikey");
request.AddHeader("", "

");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```python
import http.client

conn = http.client.HTTPSConnection("api.atmosbot.com")
payload = ''
headers = {
  'x-atmos-key': 'youratmosapikey',
  '': '

'
}
conn.request("GET", "/v1/<exchange>/<symbol>/ohlcv/latest", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```shell
curl "http://api.atmosbot.com/v1/<exchange>/<symbol>/ohlcv/latest" \
  -H "Authorization: youratmosapikey"
```

```javascript

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function() {
  if(this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.atmosbot.com/v1/<exchange>/<symbol>/ohlcv/latest");
xhr.setRequestHeader("x-atmos-key", "youratmosapikey");
xhr.setRequestHeader("", "\n\n");

xhr.send();
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

`GET /v1/<exchange>/<symbol>/ohlcv/latest`



