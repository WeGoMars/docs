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
    "message": "인증에 성공했습니다. 비밀번호를 재설정할 수 있습니다."
}
```
- response: 400 실패시1(인증번호 X)
```
{
    "status": "false",
    "message": "인증번호가 일치하지 않습니다."
}
```
- response: 400 실패시2 (이메일 X)
```
{
    "status": "false",
    "message": "해당 이메일로 등록된 사용자가 없습니다."
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
    "token": "jwt_token" _ex:"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.."
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
- method: POST
- endpoint: http://{server}:4000/login
- header: Content-Type: application/json
- Authorization: Bearer {jwt_token}
- body:
```
{}
```
- response: 200 OK (로그아웃 성공)
```
{  
    "status": "success",
    "message": "Logout successful."
}
```
- response: 401 Unauthorized (토큰 없음 또는 만료)
```
{
    "status": "false",
    "message": "Unauthorized request."
}
```