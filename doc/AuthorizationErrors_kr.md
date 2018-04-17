# Thing+ OAuth2 Authorization Errors
Thing+ OAuth2 Authorization Errors 는 인증 요청 에러, 액세스 토큰 요청 에러, 액세스 토큰을 포함한 API 요청 에러에 대한 **에러 메시지 세부정보**를 제공합니다.

## 인증 요청 에러
### 필수 파라미터 누락
client_id 또는 response_type 또는 redirect_uri가 없으면 code invalid_request 인 AuthorizationError 가 발생합니다.
```json
{
  "name": "AuthorizationError",
  "message": "Missing required parameter: response_type",
  "code": "invalid_request",
  "status": 400
}
```

### 지원되지 않는 응답 타입
지원되지 않는 응답 타입으로 요청하면 code unsupported_response_type 인 AuthorizationError 가 발생합니다.
```json
{
  "name": "AuthorizationError",
  "message": "Unsupported response type: code2",
  "code": "unsupported_response_type",
  "status": 501
}
```

### 허용되지 않은 클라이언트 아이디
client_id가 없거나 허용되지 않은 클라이언트 아이디일 경우 code unauthorized_client 인 AuthorizationError 가 발생합니다.
```json
{
  "name": "AuthorizationError",
  "message": "The client_id is incorrect",
  "code": "incorrect_client_credentials",
  "status": 401
}
```

### 일치하지 않는 리디렉션 URI
애플리케이션에 등록한 redirect_uri와 요청된 redirect_uri가 일치하지 않으면 code redirect_uri_mismatch 인 AuthorizationError 가 발생합니다.
```json
{
  "name": "AuthorizationError",
  "message": "Mismatched redirect_uri",
  "code": "redirect_uri_mismatch",
  "status": 400
}
```

### 사용자 요청 거부
사용자가 요청을 거부하면 URI에 access_denied 를 포함하여 리디렉션됩니다.
```json
{REDIRECT_URI}/?error=access_denied
```

### 허용되지 않은 요청
사용자가 권한 부여 페이지에서 수락하고 같은 페이지에서 한 번 더 수락하면 ForbiddenError 가 발생합니다.
```json
{
  "name": "ForbiddenError",
  "message": "Unable to load OAuth 2.0 transaction: xxffggxxaf",
  "status": 403
}
```

## 액세스 토큰 요청 에러
### 지원되지 않는 grant_type
지원되지 않는 grant_type으로 요청하면 code unsupported_grant_type 인 TokenError 가 발생합니다.
```json
{
  "name": "TokenError",
  "message": "Unsupported grant type: password2",
  "code": "unsupported_grant_type",
  "status": 501
}
```

### 만료된 인증 코드
인증 코드가 만료되면 code expired_code 인 TokenError 가 발생합니다.
```json
{
  "name": "TokenError",
  "message": "Authorization code is expired",
  "code": "expired_code",
  "status": 403
}
```

### 유효하지 않은 인증 코드
인증 코드가 올바르지 않으면 code invalid_code 인 TokenError 가 발생합니다.
```json
{
  "name": "TokenError",
  "message": "Authorization Code is invalid",
  "code": "invalid_code",
  "status": 400
}
```

### 일치하지 않는 리디렉션 URI
응용 프로그램에 등록한 redirect_uri가 요청 redirect_uri와 일치하지 않으면 code redirect_uri_mismatch 인 TokenError 가 발생합니다.
```json
{
  "name": "TokenError",
  "message": "Mismatched redirect_uri",
  "code": "redirect_uri_mismatch",
  "status": 400
}
```

### 올바르지 않은 클라이언트 자격 증명
client_id 또는 client_secret이 올바르지 않으면 code incorrect_client_credentials 인 TokenError 가 발생합니다.
```json
{
  "name": "TokenError",
  "message": "The client_id and/or client_secret are incorrect",
  "code": "incorrect_client_credentials",
  "status": 401
}
```

### 올바르지 않은 사용자 자격 증명
사용자 이름 또는 암호가 올바르지 않으면 code incorrect_user_credentials 인 TokenError 가 발생합니다.
```json
{
  "name": "TokenError",
  "message": "The username and/or password are incorrect",
  "code": "incorrect_user_credentials",
  "uri": null,
  "status": 401
}
```

### 승인되지 않은 사용자
승인되지 않은 사용자인 경우 code unauthorized_user 인 TokenError 가 발생합니다.
```json
{
  "name": "TokenError",
  "message": "The user is unauthorized",
  "code": "unauthorized_user",
  "uri": null,
  "status": 403
}
```

## 액세스 토큰을 포함한 API 요청 에러
### 올바르지 않은 액세스 토큰
액세스 토큰이 유효하지 않거나 올바르지 않으면 JsonWebTokenError 가 발생합니다.
```json
{
  "name": "JsonWebTokenError",
  "message": "invalid token"
}
```

### 올바르지 않은 서명
Access 토큰을 생성하는 비밀 키가 변경되면 JsonWebTokenError 가 발생합니다.
> 이 에러가 발생하면 사용자로부터 새로운 AccessToken 을 획득해야합니다.
```json
{
  "name": "JsonWebTokenError",
  "message": "invalid signature"
}
```

### 만료된 액세스 토큰
액세스 토큰이 만료되면 TokenExpiredError 가 발생합니다.
```json
{
"name": "TokenExpiredError",
"message": "jwt expired",
"expiredAt": "2015-06-10T10:10:34.000Z"
}
```
