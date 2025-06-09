
# 내 종목 간략목록보기 ✔️
- 왼쪽 사이드바의 내 종목 목록보기에 쓰기 위해 사용
## 요청
```
method: GET
endpoint: /api/portfolios/list
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "your stock list",
  "data": [
    {
      "symbol": "A",
      "name": "Agilent Technologies, Inc.",
      "currentPrice": 111.84,
      "priceDelta": -0.0799999999999983
    },
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "currentPrice": 200.66,
      "priceDelta": -0.18999999999999773
    }
  ]
}
```
### 응답 파라미터
- symbol: 심볼
- createdAt: 만들어진 날짜
- currentPrice: 현재가격
- priceDelta: 전날 종가 대비 현재 가격