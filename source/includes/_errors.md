# Errors

<aside class="notice">
This section displays information related to the potential errors you could encounter whislt using Atmos API.
</aside>

> 401 Error :

```json
{
    "statusCode": 401,
    "message": "Unauthorized"
}
```

> 404 Error :

```json
{
    "statusCode": 404,
    "message": "Cannot GET /v1/<exchange>/ETHUSDT/ohlcv/abc",
    "error": "Not Found"
}
```

> 429 Error :

```json
{
    "statusCode": 429,
    "message": "You send requests too often. Please try again in a few minutes."
}
```

Atmos API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
404 | Not Found -- The specified candle could not be found.
429 | Too Many Requests -- You're requesting too many candles.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.


If your issues persist, do not hesitate to contact support.