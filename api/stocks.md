# 종목 기능
## 종목 검색
- method: POST
- endpont: http://{server}:4000/stocks/search?query={param ex:aapl}
- header: Content-Type: application/json
- body: 
```
{}
```

- response: 200
```
{
    "success": true,
    "message": "Search successful.",
    "data": [
        {
            "symbol": "AAPL",
            "name": "Apple Inc.",
            "exchange": "NASDAQ"
        },
        {
            "symbol": "AAPL.MX",
            "name": "Apple Inc.",
            "exchange": "Mexican Stock Exchange"
        }
    ]
}
```

- response: 400 실패시
```
{
  
}
```

- response: 400 실패시2 (param 값 누락)
```
{
    "success": false,
    "message": "Invalid request body. Email, password, and nick are required."
}
```

## 비밀번호 초기화 (authentication) 

- method: POST
- endpont: http://{server}:4000/stocks/resetpwd
- header: Content-Type: application/json
- body: 
```
{
    "email":"elon@mars.com",
    "code":"0000"
}
```
- response: 200
```
{
    "success": true,
    "message": "Authentication successful. You may now reset your password."
}
```
- response: 400 실패시1(인증번호 X)
```
{
    "success": false,
    "message": "Invalid authentication number."
}
```
- response: 400 실패시2 (이메일 X)
```
{
    "success": false,
    "message": "Email not found."
}
```
