# Thing+ API 이용 가이드
`Thing+` 에서 제공하는 `API`를 설명하는 문서입니다.

API를 사용하기에 앞서 [Thing+ Developer Guide](https://github.com/daliworks/thingplus-guide)를 읽는것을 권장합니다.

Thing+ 는 `3rd party`가 Thing+의 기능들을 사용 할 수 있도록 일부 기능을 Thing+ API로 제공하고 있으며
계속해서 제공 범위를 넓혀 가고 있습니다.


## 접근 리소스 범위
`Thing+ API`로 접근 가능한 리소스는 `Scope`에 의해 정해집니다.

`Scope`의 상세 내용은 [여기](./OAuth2.md#scopes)를 참조하세요


## 요구사항
`Thing+ API` 를 사용하기위해서는 각 리소스에 대한 `권한`이 필요하며
권한은 `oAuth2`를 통해 획득 할 수 있습니다.

`oAuth2`에 대한 상세 가이드는 [여기](https://github.com/daliworks/thingplus-guide/blob/master/doc/OAuth2Guide_kr.md)를 참조하시기 바랍니다.

각 리소스에 대한 권한은 `token`을 통해 이용가능합니다.

`Token` 획득을 위한 사전 준비가 필요합니다.

## 사전 준비 및 Token 획득

사전 준비로 `authClient` 생성을 해야합니다.

[authClient 생성](https://thingplus.api-docs.io/2.0/oauth2/create-authclients) 을 참고하여 `authClient`를 생성하고 해당 `authClient`를 이용하여 `token`을 획득합니다.

oAuth token 획득을 위해 현재 2가지 방법을 제공합니다.

1. [Authorization Code 방식](./OAuth2Guide_kr.md#authorization-code-방식)
2. [Resource Owner Password Credentials 방식](./OAuth2Guide_kr.md#resource-owner-password-credentials-방식)
 

획득한 토큰을 `request Header`에 넣어 이용합니다.

특정 사용자에게 리소스 권한을 위임 받기 원하는 경우에는 `1. Authorization Code grunt` 방식을 사용합니다.

특정 사용자가 아닌 관리자(Admin)의 권한으로 관리범위의 리소스에 접근하기를 원하는 경우에는 `2. Resource owner password Credentials grant` 방식을 사용합니다.

좀더 자세한 내용은 [여기](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_en.md#22-oauth앱-연동-플로우) 를 참조하세요

API Document Site에서는 편의상 `2. Resource owner password Credentials grant`를 사용 하도록 합니다.


## 유의 사항
<https://thingplus.api-docs.io> 에서는 사전 준비과정인 [Create authClients]() 를 할수가 없습니다.
 
별도의 어플리케이션을 사용하여 `authClient`를 생성해 주세요.

생성 과정은 [여기](./GettingStartedWithHttpsAndOauth.md) 에서 자세한 설명을 하고 있으며
[따라하기](./GettingStarted_authToken.md) 링크 에서 `authClient` 생성하는 과정을 보여주고 있습니다

성공적으로 `authClient`를 생성 했다면 이제 <https://thingplus.api-docs.io> 에서 `request try`를 이용하여 실제 요청을 할 수 있습니다.

[OAuth2Token - Resource Owner Password Credentials Grant](https://thingplus.api-docs.io/2.0/oauth2/oauth2token-1)로 이동한 후 생성한 `authClient`를 이용해 `OAuth Token`을 획득해 보세요
 
## 사용방법

획득한 `Token`을 `Request Header`에 넣어 사용합니다.

Token API `response`의 `token_type`과 `access_token`를 이용합니다.

`Header`에 `Authorization` 필드를 추가하고 `{token_type} {access_token}` 형태로 값을 입력합니다.

ex) Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.ezcxfQ.BfgfVvKhvTOwlYHSzcFPQl-0c

[Get My Account](https://thingplus.api-docs.io/2.0/users/get-my-account) API를 통해 권한을 획득한 User의 정보를 확인해 봅시다.


성공적으로 `Response` 를 받았다면 모두 정상적으로 준비 되었습니다.

다른 API를 살펴보고 테스트해보세요.

각 API의 파라미터 및 자세한 설명은 <https://thingplus.api-docs.io/2.0> 를 참고하세요.

### 1. Add Gateway/Sensor
게이트웨이/센서를 등록하기 위해 몇가지 과정이 필요할 수 있습니다.
[여기](./registerGateway_kr)에 자세한 설명이 있습니다.

### 2. Read Gateway
게이트웨이의 목록과 정보를 읽어오기 위한 API 입니다.

Collection을 가져오기 위한 API 와 단일 Resource를 가져오기 위한 API를 제공합니다.

1. [게이트웨이 Collection](https://thingplus.api-docs.io/2.0/gateways/list-gateways)
2. [특정 게이트웨이](https://thingplus.api-docs.io/2.0/gateways/get-gateway)

#### 2.1 Read Gateway Status
게이트웨이 상태를 가져오기 위한 API 입니다.

query 에 날짜를 추가하여 기간내의 data를 배열로 가져 올 수 있으며 default로는 마지막 값을 가져옵니다

`value`에 적용될 수 있는 값은 `on, off, err` 입니다.

https://thingplus.api-docs.io/2.0/gateway-status/get-gateway-status

### 3. Read Sensor
게이트웨이에 연결된 센서들의 정보를 가져오기 위한 API 입니다

Collection을 가져오기 위한 API 와 단일 Resource를 가져오기 위한 API를 제공합니다.

1. [게이트웨이 Collection](https://thingplus.api-docs.io/2.0/gateway-sensors/list-gateway-sensors)
2. [특정 게이트웨이](https://thingplus.api-docs.io/2.0/gateway-sensors/get-gateway-sensors)

#### 3.1 Read Sensor Status
센서의 상태를 가져오기 위한 API 입니다.

마지막 상태 값을 가져오며 `value`에 적용될 수 있는 값은 `on, off, err` 입니다.

https://thingplus.api-docs.io/2.0/sensor-status/get-sensor-status


#### 3.2 Read Sensor Series (Sensor value)
센서의 값을 가져오기 위한 API 입니다.

`query` 에 날짜를 추가하여 기간내의 data를 배열로 가져 올 수 있으며 default 는 마지막 값을 가져옵니다

`query` 를 이용하여 통계값도 확인 할 수 있으며 통계를 위한 `interval` 조절도 가능합니다

https://thingplus.api-docs.io/2.0/sensor-series/get-sensor-series


### 4. 응용
`queryString`을 이용하여 다양한 이용이 가능합니다.

`Filter`를 이용하여 특정 조건에 부합되는 정보만 획득 할 수 있으며 `fields`를 이용하여 특정 필드값만 가져올 수도 있습니다.

`embed`를 이용하여 하나의 API로 여러 API의 결과와 동일한 정보를 가져 올 수 있습니다


https://thingplus.api-docs.io/2.0/getting-started/query-string

### 5. Control Actuator
`Actuator` 에 명령을 보내 동작을 시킬 때 사용 합니다.

해당 기능을 이용하기 위해서는 목표 센서의 `update` 권한이 있어야만 합니다

https://thingplus.api-docs.io/2.0/non-rest-apis/controlactuator


### 6. Manage Gateway
게이트웨이를 재시작하거나 종료시키는 등 게이트웨이에 특정 명령을 보내기 위해 사용합니다

해당 기능을 위해 목표 게이트웨이의 `update` 권한이 있어야만 합니다.

https://thingplus.api-docs.io/2.0/non-rest-apis/managegateway


### 7. Push Device

### 8. Rule
