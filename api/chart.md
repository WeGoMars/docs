# 주식 차트 데이터 API

# 차트 데이터 조회

```
method: GET
endpoint: http://{server}:4000/stocks/chart?symbol={symbol}&interval={interval}&limit={limit}
header: Content-Type: application/json
parameters:
symbol: 종목 코드 (예: AAPL)
interval: 차트 기간 (1h,1day,1week,1month)
limit:몇 개의 ohlcv 데이터를 가져올지(data 의 length 를 결정). 최대값은 120.
```

- response: 200
- 정렬 : 최신이 늘 data[0]
```JSON
{
    "success": true,
    "message": "AAPL's chart data",
    "data": [
        {
            "timestamp": "2025-05-30",
            "open": 199.37,
            "high": 201.96,
            "low": 196.78,
            "close": 200.85,
            "volume": 70753100
        },
        {
            "timestamp": "2025-05-29",
            "open": 203.58,
            "high": 203.81,
            "low": 198.51,
            "close": 199.95,
            "volume": 51396800
        }
    ]
}
```
- response: 400 (잘못된 기간 파라미터)
```JSON
{
  "success": false,
  "message": [
    "interval must be one of: 1hour, 1day, 1week, 1month"
  ]
}
```

- response: 404 (해당 심볼 없음)
```JSON
{
  "success": false,
  "message": "No Such Symbol : (AAPd)"
}
```

# 주식 기본 정보 API

# 종목 상세 정보 조회

```
method: GET
endpoint: http://{server}:4000/stocks/{symbol}
header: Content-Type: application/json
parameters:
symbol: 종목 코드 (예: AAPL)
```

- response: 200
```JSON
{
  "success": true,
  "message": "AAPL's detailed data",
  "data": {
    "stockId": 2,
    "symbol": "AAPL",
    "name": "Apple Inc.",
    "roe": 1.51306,
    "eps": 6.48883,
    "bps": 4.45482,
    "beta": 1.275,
    "marketCap": 2999860000000,
    "dividendYield": 0.00502863,
    "currentRatio": 0.82087,
    "debtRatio": 1.46994,
    "sector": "Technology",
    "industry": "Consumer Electronics",
    "lastPrice": 200.85,
    "currentPrice": 200.66
  }
}
```

- response: 404 (해당 심볼 없음)
```JSON
{
  "success": false,
  "message": "No Such Symbol : (AAPd)"
}
```

# 주식 검색 API

# 종목 검색

```
method: POST
endpoint: http://{server}:4000/stocks/search?query={param}
header: Content-Type: application/json
```

```

- body
{}

```

```
- response: 200
{
    "success": true,
    "message": "Search successful.",
    "data": [
        {
            "symbol": "AAPL",
            "name": "Apple Inc.",
            "price": "175.04",
            "change": "+1.23",
            "changePercent": "+0.71%"
        },
        {
            "symbol": "AAPL.MX",
            "name": "Apple Inc.",
            "price": "175.04",
            "change": "+1.23",
            "changePercent": "+0.71%"
        }
    ]
}
```

```
- response: 400 (검색어 누락)
{
    "success": false,
    "message": "Search query parameter is required"
}
```
