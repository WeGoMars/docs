
# 차트 데이터 조회 ✔️
- 캔들차트를 뽑기 위한 데이터를 요청청
```
method: GET
endpoint: /api/stocks/chart?symbol={symbol}&interval={interval}&limit={limit}
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
# 종목 상세 정보 조회 ✔️
- 정확한 심볼 정보를 req, 자세한 주식종목정보를 res 
```
method: GET
endpoint: /api/stocks/{symbol}
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

# 주식 종목 검색 ✔️
-심볼 문자열의 일부를 req, 해당 문자열을 이름 or symbol에 포함한 주식을 최대 limit 개 배열에 담아 res

```
method: GET
endpoint: /api/stocks/search?query={query}&limit={limit}
```
```
query : 검색 조건이 될 문자열(심볼, 네임 어느쪽이든 가능, 아래는 AA로 검색한 예시)
limit : 숫자, 최대 20건
```

- response: 200
```JSON
{
  "success": true,
  "message": "search succesful",
  "data": [
    {
      "symbol": "A",
      "name": "Agilent Technologies, Inc.",
      "sector": "Healthcare",
      "industry": "Diagnostics & Research",
      "currentPrice": 111.84,
      "priceDelta": -0.0799999999999983
    },
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "sector": "Technology",
      "industry": "Consumer Electronics",
      "currentPrice": 200.66,
      "priceDelta": -0.18999999999999773
    }
  ]
}
```
```
pricedelta : 어제 종가 - 현재가. 주식정보 제공 사이트들은 보통 어제 종가 대비 얼마나 변화했나를 퍼센트로 나타낸다고 한다. 만약 퍼센트로 표시하고 싶다면 계산이 필요.
```

```
- response: 400 (검색어 누락)
{
    "success": false,
    "message": "Search query parameter is required"
}
```
