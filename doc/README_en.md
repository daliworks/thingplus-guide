# Thing+ Guide
용어설명을 읽고 플로우를 따라 개발을 진행해보세요.
아직 장비가 없다해도 간단한 시뮬레이터를 제공하고 있습니다.

`SandBox` 는 상용서비스에 미반영된 기능이 일부 있을 수 있으며 중단 될 수 있습니다.<br>
정식 서비스는 별도로 문의를 해주세요 <contact@thingplus.net>

## Conents
* [용어 설명](#1-용어-설명)
* [장비 연동 플로우](#2-장비-연동-플로우)
* [임베디드 개발 가이드](#3-임베디드-개발-가이드)
* [oAuth/앱 연동 플로우](#4-oauth앱-연동-플로우)
* [oAuth 개발 가이드](#5-oauth-개발-가이드)
* [API 문서](#6-api-문서)
* [Portal 사용 가이드](#7-portal-사용-가이드)
* [타 IoT 플렛폼 연동 플로우](#8-타-iot-플렛폼-연동-플로우)

## 1. 용어 설명

| Term | Description | example
| --- | --- | ----
| Sensor | the hw to collect some value or state<br>Defiend All sensor include Actuator | temperature, humidity
| Actuator | the hw to input command from outside | camera, switch
| Device | Group of Sensor. Sometime the group is virtual but some time is real<br> Gateway have to composed by at least one device |
| Gateway | HW / SW to communicate with server <br> send sensor value/status to server or forward command from server to sensor |
| Tag | 여러 디바이스/게이트웨이에 흩어져 존재하는 Sensor를 그룹화하여 관리 할 수 있는 단위 |
| oAuth2 | 권한 인증을 수행할 수 있는 표준 Open Protocol | 
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
1. example about Gateway/Device/Sensor/Tag
    * 라즈베리파이 IoT 스타터 킷을 이용한 Home IoT. 이때 온습도 센서가 2개씩 있다고 가정
        * Sensor - temperature sensor, humidity sensor
        * Actuator - Led sensor that can be turn on/off
        * Device - RaspberryPi Starter Kit
        * Gateway - RaspberryPi
        * Tag - temperature sensor 1, humidity sensor1 Tagged `Room`, temperature sensor 2, humidity sensor2 Taggged `Living Room`


## 2. Flow for interworking hardware(embedded)
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/[en]flow_for_hardware_v1.1.pdf)

## 3. embedded Development Guide
[Link](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide_EN.md)

## 4. Flow for interworking oAuth/App
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/[en]flow_for_app_with_oauth2_v1.1.pdf)

## 5. oAuth Development Guide
[Link](./oAuth2Guide_en.md)

## 6. API document
[Link](https://thingplus-10.api-docs.io/2.0/)

#### 6.1 Test URL
https://www.sandbox.thingplus.net/

#### 6.2 Response Status Code
basically the http response status code is the same

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
| REQUEST_ERROR | NOT_FOUND | resource not found
| REQUEST_ERROR | MISMATCH_ERROR | request value is not equal value in DB
| REQUEST_ERROR | CONFLICT | already exist
| REQUEST_ERROR | INVALID_INPUT | wrong parameter
| AUTHENTICATION_ERROR | NEED_LOGIN | need login
| AUTHORIZATION_ERROR | ACCESSGROUP_DENY | ACL deny
| AUTHORIZATION_ERROR | ACL_DENY | ACL deny
| SERVER_ERROR | JSON_PARSING | json parsing exception
| SERVER_ERROR | USER_ERROR | internal error
| SERVER_ERROR | AUTH_ERROR | internal error
| SERVER_ERROR | ACL_ERROR | internal error
| SERVER_ERROR | LIBRARY_ERROR | internal error
| SERVER_ERROR | INTERNAL_ERROR | internal error
| DB_ERROR | RELATION_ERROR | internal error
| DB_ERROR | QUERY_RESULT_EMPTY | internal error
| DB_ERROR | NOT_FOUND_IN_ITEM | internal error
| DB_ERROR | DB_INTERNAL_ERROR | internal error
| BILLING_ERROR | BILLING | need increase billing
| GATEWAY_ERROR | PROCESS_COMMAND_RESULT | unknown error when receive result from gateway
| UNKNOWN | - |



## 7. Portal Use Guide
[To be provided later]

## 8. Flow for interworking another Iot platform
[To be provided later]

## Changes history


## License
