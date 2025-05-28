# 회원 기능
## 회원가입
- method: POST
- endpont: http://{server}:4000/signup
- header: Content-Type: application/json
- body: 
```
{
    "email":"elon@mars.com",
    "password":"wegomars",
    "nick":"doge1"
}
```

- response: 200
```
{
    "success": true,
    "message": "User registered successfully.",
    "user": {
        "id": 1,
        "email": "elon@mars.com",
        "nick": "doge1"
    }
}
```

- response: 400 실패시1 (이메일 중복)
```
{
    "success": false,
    "message": "Email already in use."
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
- endpont: http://{server}:4000/resetpwd
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
    "message": "인증에 성공했습니다. 비밀번호를 재설정할 수 있습니다."
}
```
- response: 400 실패시1(인증번호 X)
```
{
    "success": false,
    "message": "인증번호가 일치하지 않습니다."
}
```
- response: 400 실패시2 (이메일 X)
```
{
    "success": false,
    "message": "해당 이메일로 등록된 사용자가 없습니다."
}
```
