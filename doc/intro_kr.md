## 소개
Thing+ 에서 제공하는 API를 설명하는 문서입니다.

API를 사용하기에 앞서 [Thing+ Developer Guide](https://github.com/daliworks/thingplus-guide)를 읽는것을 권장합니다.

`3rd party`가 Thing+에서 제공하는 기능들을 사용 할 수 있도록 일부 기능을 Thing+ API로 Open하였으며 Open범위를 계속 넓혀 가고 있습니다


## 가능 범위
Thing+ API로 접근 가능한 리소스는 Scope에 의해 정해집니다.

Scope의 상세 내용은 #docTextSection:3T3twjpBjxwMyo6Xs 를 참조하세요


## 요구사항
Thing+ API 를 사용하기위해서는 각 리소스에 대한 권한이 필요하며 
권한은 `OAuth2`를 통해 획득 할 수 있습니다.

`OAuth2`에 대한 상세 가이드는 [여기](https://github.com/daliworks/thingplus-guide/blob/master/doc/OAuth2Guide_en.md)를 참조하시기 바랍니다.

각 리소스에 대한 권한은 `token`을 통해 이용가능합니다.

`Token` 획득을 위한 사전 준비가 필요합니다.

## 사전 준비 및 Token 획득

사전 준비로 `authClient` 생성을 해야합니다.

#endpoint:rQi8KjEqgw4J2HBy6 를 이용하여 `authClient`를 생성하고 해당 `authClient`를 이용하여 `token`을 획득합니다.

OAuth token 획득을 위해 현재 2가지 방법을 제공합니다.

1. #endpoint:Pv7MmRuhWcoXziFPa
2. #endpoint:7RcNk9pBovabaZL96
 

획득한 토큰을 `request Header`에 넣어 이용합니다.

특정 사용자에게 리소스 권한을 위임 받기 원하는 경우에는 `1. Authorization Code grunt` 방식을 사용합니다.

특정 사용자가 아닌 관리자(Admin)의 권한으로 관리범위의 리소스에 접근하기를 원하는 경우에는 `2. Resource owner password Credentials grant` 방식을 사용합니다.

좀더 자세한 내용은 [여기](
https://github.com/daliworks/thingplus-guide/blob/master/doc/README_en.md#22-for-utilizing-oauthapp) 를 참조하세요

API Document Site에서는 편의상 `2. Resource owner password Credentials grant`를 사용 하도록 합니다.



## 유의 사항
<https://thingplus.api-docs.io> 에서는 사전 준비과정인 #endpoint:rQi8KjEqgw4J2HBy6 를 할수가 없습니다.
 
별도의 어플리케이션을 사용하여 `authClient`를 생성해 주세요.

[따라하기](http://support.thingplus.net/en/rest-api/getting-started.html#id-step1) 링크 에서 `authClient`생성하는 방법을 자세히 설명하고 있습니다.

성공적으로 `authClient`를 생성 했다면 이제 <https://thingplus.api-docs.io> 에서 `request try`를 이용하여 실제 요청을 할 수 있습니다.

#endpoint:7RcNk9pBovabaZL96 로 이동한 후 생성한 `authClient`를 이용해 `OAuth Token`을 획득해 보세요
 
## 사용방법

획득한 `Token`을 `Request Header`에 넣어 사용합니다.

Token API `response`의 `token_type`과 `access_token`를 이용합니다.

`Header`에 `Authorization` 필드를 추가하고 `{token_type} {access_token}` 형태로 값을 입력합니다.

ex) Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.ezcxfQ.BfgfVvKhvTOwlYHSzcFPQl-0c

#endpoint:kwgNXKGY94NMQvfcX API를 통해 권한을 획득한 User의 정보를 확인해 봅시다.


성공적으로 `Response` 를 받았다면 모두 정상적으로 준비 되었습니다.

다른 API를 살펴보고 테스트해보세요.
