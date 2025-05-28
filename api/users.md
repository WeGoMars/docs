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
    "status": "success",
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
    "status": "false",
    "message": "Email already in use."
}
```

- response: 400 실패시2 (param 값 누락)
```
{
    "status": "false",
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
    "status": "success",
    "message": "Authentication successful. You can reset your password."
}
```
- response: 400 실패시1(인증번호 X)
```
{
    "status": "false",
    "message": "The verification code does not match."
}
```
- response: 400 실패시2 (이메일 X)
```
{
    "status": "false",
    "message": "No user is registered with the provided email."
}
```

## 로그인
- method: POST
- endpoint: http://{server}:4000/login
- header: Content-Type: application/json
- body:
```
{
    "email": "elon@mars.com",
    "password": "wegomars"
}
```
- response: 200
```
{
    "status": "success",
    "message": "Login successful.",
}
```
- response: 400(입력 누락)
```
{
    "status": "false",
    "message": "Email and password are required."
}
```
- response: 401(입력 불일치)
```
{
    "status": "false",
    "message": "Invalid email or password."
}
```

## 로그아웃
- method: GET
- endpoint: http://{server}:4000/logout
- response: 200 OK (로그아웃 성공)
```
{  
    "status": "success",
    "message": "Logout successful."
}
```
- response: 401 Unauthorized (세션 없음 또는 만료)
```
{
    "status": "false",
    "message": "Unauthorized request."
}
```