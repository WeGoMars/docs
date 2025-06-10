# 유저 선호 추가 ✔️
- ai추천에 사용하기 위해 유저의 개인화된 선호를 입력받아 db에 저장하기 위한 api
- upsert 기반으로 동작(없으면 만들고, 재요청시 업데이트함)
## 요청
```
method: POST
endpoint: /api/ai/preference
header: Content-Type: application/json
제약 조건 : 로그인 필수
```
- body: 
```JSON
{
  "riskLevel": "high",
  "preferredStrategies": ["dividend_stability", "portfolio_balance", "value_stability", "momentum", "sector_rotation", "rebound_buy"],
  "preferredSectors" : ["Basic Materials", "Communication Services", "Consumer Cyclical", "Consumer Defensive", "Energy", "Financial Services", "Healthcare", "Industrials", "Real Estate", "Technology", "Utilities" ]
}
```
## 요청 파라미터
- riskLevel : high 나 low 중 1택.
- preferredStrategies : 위 예시에 나온 6중 n 택(최소 0)
- preferredSectors : 위 예시에 나온 11중 n 택(최소 0)

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "user preference saved!",
  "data": {
    "riskLevel": "high",
    "preferredStrategies": [
      "dividend_stability",
      "portfolio_balance",
      "value_stability",
      "momentum",
      "sector_rotation",
      "rebound_buy"
    ],
    "preferredSectors": [
      "Basic Materials",
      "Communication Services",
      "Consumer Cyclical",
      "Consumer Defensive",
      "Energy",
      "Financial Services",
      "Healthcare",
      "Industrials",
      "Real Estate",
      "Technology",
      "Utilities"
    ],
    "createdAt": "2025-06-09T15:59:48.324Z",
    "updatedAt": "2025-06-09T17:57:23.000Z"
  }
}
```



# 내 선호 조회 ✔️
## 요청
```
method: GET
endpoint: /api/ai/preference
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "this is your user preference",
  "data": {
    "riskLevel": "high",
    "preferredStrategies": [
      "dividend_stability",
      "portfolio_balance",
      "value_stability",
      "momentum",
      "sector_rotation",
      "rebound_buy"
    ],
    "preferredSectors": [
      "Basic Materials",
      "Communication Services",
      "Consumer Cyclical",
      "Consumer Defensive",
      "Energy",
      "Financial Services",
      "Healthcare",
      "Industrials",
      "Real Estate",
      "Technology",
      "Utilities"
    ],
    "createdAt": "2025-06-09T15:59:48.324Z",
    "updatedAt": "2025-06-09T17:57:23.000Z"
  }
}
```
### 응답 파라미터
- symbol: 심볼
- createdAt: 만들어진 날짜
- currentPrice: 현재가격
- priceDelta: 전날 종가 대비 현재 가격