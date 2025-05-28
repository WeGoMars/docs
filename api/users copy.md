# 회원 기능
## 회원가입
- method: POST
- endpont: http://{server}:4000/users/signup
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
- endpont: http://{server}:4000/users/resetpwd
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
