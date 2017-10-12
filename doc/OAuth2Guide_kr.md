# Thing+ OAuth2 가이드
3rd party에서 Thing+ 자원을(resource) 이용하기 위해
OAuth2 를 이용하여 authentication/authorization 획득 과정에 대한 간단한 가이드이다.
상세한 내용은 [여기](./OAuth2.md) 에서 설명한다.


## What is OAuth2
https://oauth.net/2/

![OAuth](./images/oauth2.png "OAuth")


## 사전 준비
1. API를 테스트 하기 위한 툴
    - Postman: https://www.getpostman.com/
    - Fiddler: http://www.telerik.com/fiddler
    - DHC: https://client.restlet.com/
2. authClient 생성
    - api guide의 authClients 항목을 참조하여 authClient를 생성
    - 생성된 authClient 에 대하여 별도 유지/관리 필요
    - authClient 생성시 사용할 `scope`는 [여기](./OAuth2.md#scopes)를 참조
 
 
## [Authorization Code 방식](./OAuth2.md#authorization-code-grant-or-web-server)
특정 user의 지정된 권한에 대한 위임을 받는다.
별도의 앱/웹에서 유저별로 관리가 필요할 경우 사용한다.

추가 요청시 oAuth Login 페이지에 대한 customizing 이 가능하다.

1. oauth2/authorize API를 통해 thing+ page 이동
1. 로그인이 되어 있지 않을경우 Login. 이미 로그인이 되어있다면 다음 단계로
1. Redirect 된 URL의 query에서 code 를 획득
1. oauth2/token API를 통해 access_token 획득
    * 해당 토큰은 15일간 유효하며 유지/관리가 필요하다
1. 획득한 토큰을 API에서 이용한다
    * Request Header 에 Authorization 필드 추가
    * Value에 token API response의 Token_Type과 access_token 활용 값을 채움
    * {token_type} {access_token} 형태
    * ```Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiIyIiwiY2xpZW50SWQiOiJzd2l0aGVyIiwiaWF0IjoxNDkxMjc1MTMxLCJleHAiOjE0OTI1NzExMzF9.bG1pusWH5pwJ4_BxQ-v0tmgkqMix3H82uUSxZycBWOo```
1. 위의 과정을 이용하여 개발한다



## [Resource Owner Password Credentials 방식](./OAuth2.md#resource-owner-password-credentials-grant)
serviceAdmin 의 권한으로 서비스내 리소스를 접근한다.

1. oauth2/token API를 통해 access_token 획득
    * 해당 토큰은 90일간 유효하며 유지/관리가 필요하다
1. 획득한 토큰을 API에서 이용한다
    * Request Header 에 Authorization 필드 추가
    * Value에 token API response의 Token_Type과 access_token 활용 값을 채움
    * {token_type} {access_token} 형태
    * ```Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiIyIiwiY2xpZW50SWQiOiJzd2l0aGVyIiwiaWF0IjoxNDkxMjc1MTMxLCJleHAiOjE0OTI1NzExMzF9.bG1pusWH5pwJ4_BxQ-v0tmgkqMix3H82uUSxZycBWOo```
1. 위의 과정을 이용하여 개발한다
1. serviceAdmin으로 리소스 접근시 여러 사용자의 데이터가 접근됨으로 해당 기능을 고려하여 개발한다

## 상세 설명
[Link](./OAuth2.md)

