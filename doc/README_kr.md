# Thing+ 가이드
용어설명을 읽고 플로우를 따라 개발을 진행해보세요.
아직 장비가 없다해도 간단한 시뮬레이터를 제공하고 있습니다.

`SandBox` 는 상용서비스에 미반영된 기능이 일부 있을 수 있으며 중단 될 수 있습니다.<br>
정식 서비스는 별도로 문의를 해주세요 <contact@thingplus.net>

## Conents
* [용어 설명](#1-용어-설명)
* [장비 연동 플로우](#2-장비-연동-플로우)
* [임베디드 개발 가이드](#3-임베디드-개발-가이드)
* [OAuth/앱 연동 플로우](#4-oauth앱-연동-플로우)
* [OAuth 개발 가이드](#5-oauth-개발-가이드)
* [API 문서](#6-api-문서)
* [Portal 사용 가이드](#7-portal-사용-가이드)
* [타 IoT 플렛폼 연동 플로우](#8-타-iot-플렛폼-연동-플로우)

## 1. 용어 설명

| 용어 | 용어 설명 | 예
| --- | --- | ----
| Sensor | 특정 값을 수집/전송/상태를 감지하는 HW <br>Actuator를 포함한 모든 센서를 Sensor로 정의 | 온도, 습도 센서 등
| Actuator | 외부 입력을 받아 특정한 동작이 가능한 HW | 조명스위치, 카메라, 가스벨브스위치 등
| Device | 센서의 그룹. 가상의 그룹 또는 실제 HW 로 구성된 그룹 <br>게이트웨이는 최소 1개 이상의 디바이스를 처리 |
| Gateway | 서버와 통신을 하는 HW/SW <br>센서값/상태를 서버로 전달하거나 서버로부터 센서로 명령을 전달 |
| Sensor Type | 센서 측정값의 물리량에 따라 센서를 분류한 것. 센서 타입에 따라 서비스에서 표시되는 형태(단위, 아이콘 등)가 달라지며, 설정 가능한 규칙 또한 달라질 수 있음 | temperature, humidity 등
| Tag | 여러 디바이스/게이트웨이에 흩어져 존재하는 Sensor를 그룹화하여 관리 할 수 있는 단위 |
| OAuth2 | 권한 인증을 수행할 수 있는 표준 Open Protocol |
| Service | IoT서비스를 하려는 기업이 제공하는 전체 서비스 |
| Site | 서비스 내부의 관리 그룹 또는 유저의 그룹 |
| 관리자 | 서비스 또는 사이트를 관리하는 관리자 |
| 사용자 | Site에 등록 되어있는 모든 사용자 |
| 규칙 | 특정 조건에 따라서 원하는 기능을 자동으로 실행하는 기능 | 온도 10도 이하일 때 보일러 turn on


#### 1.1 추가 설명

1. Service/Site 예시
    * 학교의 각 교실의 온/습도를 모니터링 IoT
        * Service - 학교 온습도 서비스
        * Site - 각각의 교실을 사이트로 구분
        * Service Admin - 해당 서비스를 제공하는 업체 관리자
        * Site Admin - 각 교실에 측정기를 관리 하는 관리자 (ex: 선생님)
        * User - 모든 학생. 각 교실별 온도를 웹사이트/앱을 통해 확인
    * 아파트의 각 동별/호수별 전기사용량을 측정/분석하는 IoT
        * Service - 전기사용량 서비스
        * Site - 아파트 각 동을 사이트로 구분
        * Service Admin - 해당 서비스를 제공하는 업체 관리자
        * Site Admin - 각 동별 전기흐름을 관리하는 관리실 직원
        * User - 아파트 거주민. 본인의 집 전기 사용량을 확인
1. Gateway/Device/Sensor/Tag 예시
    * 라즈베리파이 IoT 스타터 킷을 이용한 Home IoT. 이때 온습도 센서가 2개씩 있다고 가정
        * Sensor - 온도 센서, 습도 센서
        * Actuator - Led 센서
        * Device - 라즈베리파이 스타터킷
        * Gateway - 라즈베리파이
        * Tag - 온도센서1, 습도센서1을 Tag Room, 온도센서2, 습도센서2를 Tag Living Room


## 2. 장비 연동 플로우
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Bkr%5DWorkflow%20for%20hardware%20interlock_v1.2.pdf)


## 3. 임베디드 개발 가이드
[Link](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide.md)

## 4. OAuth/앱 연동 플로우
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Bkr%5Dworkflow%20for%20utilizing%20oauth_v1.2.pdf)

## 5. OAuth 개발 가이드
[Link](./OAuth2Guide_kr.md)

## 6. API 문서
[Link](https://thingplus-10.api-docs.io/2.0/)

#### 6.1 Test URL
https://nocert.sandbox.thingplus.net/

#### 6.2 Response Status Code
기본적으로 http response status code 동일

| StatusCode | Description
| --- | ---
| 200 | OK
| 201 | Created
| 204 | No Content
| 207 | Multi-Status
| 400 | Bad Request
| 401 | Unauthorized
| 403 | Forbidden
| 404 | Not Found
| 409 | Conflict
| 429 | Too Many Requests
| 444 | Unknown
| 471 | Billing (Temporary)
| 500 | Internal Server Error
| 504 | Gateway Time-out
| 600 | Gateway Error


#### 6.3 API Error Code
Thing+ API Error Category & Code is `string`

| Category | Code | Description
| --- | --- | ---
| REQUEST_ERROR | SCHEMA_VALIDATE | validate schema fail
|  | NOT_FOUND | resource not found
|  | MISMATCH_ERROR | request value is not equal value in DB
|  | CONFLICT | already exist
|  | INVALID_INPUT | wrong parameter
| AUTHENTICATION_ERROR | NEED_LOGIN | need login
| AUTHORIZATION_ERROR | ACCESSGROUP_DENY | ACL deny
|  | ACL_DENY | ACL deny
| SERVER_ERROR | JSON_PARSING | json parsing exception
|  | USER_ERROR | internal error
|  | AUTH_ERROR | internal error
|  | ACL_ERROR | internal error
|  | LIBRARY_ERROR | internal error
|  | INTERNAL_ERROR | internal error
| DB_ERROR | RELATION_ERROR | internal error
|  | QUERY_RESULT_EMPTY | internal error
|  | NOT_FOUND_IN_ITEM | internal error
|  | DB_INTERNAL_ERROR | internal error
| BILLING_ERROR | BILLING | need increase billing
| GATEWAY_ERROR | PROCESS_COMMAND_RESULT | unknown error when receive result from gateway
| UNKNOWN | - |



## 7. Portal 사용 가이드
[Link](http://support.thingplus.net/ko/user-guide/registration.html#id-enduser)

## 8. 타 IoT 플랫폼 연동 플로우
[추후 제공]

## Changes history


## License
