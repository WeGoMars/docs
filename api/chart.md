# 주식 차트 데이터 API

# 차트 데이터 조회

```
method: GET
endpoint: http://{server}:4000/stocks/{symbol}/chart?period={period}
header: Content-Type: application/json
parameters:
symbol: 종목 코드 (예: AAPL)
period: 차트 기간 (daily, weekly, monthly, minutes)
```

```
- response: 200
{
    "success": true,
    "message": "Chart data retrieved successfully.",
    "data": {
        "prices": [
            {
                "date": "2024-03-20T00:00:00Z",
                "value": 175.04
            },
            {
                "date": "2024-03-19T00:00:00Z",
                "value": 173.23
            }
        ],
        "volumes": [
            {
                "date": "2024-03-20T00:00:00Z",
                "value": 52345678
            },
            {
                "date": "2024-03-19T00:00:00Z",
                "value": 48912345
            }
        ]
    }
}
```

```
- response: 400 (잘못된 기간 파라미터)
{
    "success": false,
    "message": "Invalid period parameter. Must be one of: daily, weekly, monthly, minutes"
}
```

```
- response: 404 (종목을 찾을 수 없음)
{
    "success": false,
    "message": "Stock symbol not found"
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

```
- response: 200
{
    "success": true,
    "message": "Stock information retrieved successfully.",
    "data": {
        "symbol": "AAPL",
        "name": "Apple Inc.",
        "price": "175.04",
        "change": "+1.23",
        "changePercent": "+0.71%",
        "volume": "52.3M",
        "marketCap": "2.8T",
        "description": "Apple Inc. is an American multinational technology company."
    }
}
```

```
- response: 404 (종목을 찾을 수 없음)
{
    "success": false,
    "message": "Stock symbol not found"
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
