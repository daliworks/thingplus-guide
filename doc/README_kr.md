# Thing+ 가이드
용어설명을 읽고 플로우를 따라 개발을 진행해보세요.
아직 장비가 없다해도 간단한 시뮬레이터를 제공하고 있습니다.

`SandBox` 는 상용서비스에 미반영된 기능이 일부 있을 수 있으며 중단 될 수 있습니다.<br>
정식 서비스는 별도로 문의를 해주세요 <contact@thingplus.net>

## Contents
* [1. 용어 설명](#1-용어-설명)
* [2. 워크플로우](#2-워크플로우)
  * [2.1 장비 연동 플로우](#21-장비-연동-플로우)
  * [2.2 OAuth/앱 연동 플로우](#22-oauth앱-연동-플로우)
  * [2.3 타 IoT 플랫폼 연동 플로우](#23-타-iot-플랫폼-연동-플로우)
* [3. 가이드](#3-가이드)
  * [3.1 센서 타입](#31-센서-타입)
  * [3.2 센서 타입 정의를 위한 고객 입력 폼](#32-센서-타입-정의를-위한-고객-입력-폼)
  * [3.3 Thing+에 등록된 게이트웨이 모델 리스트](#33-thing에-등록된-게이트웨이-모델-리스트)
  * [3.4 게이트웨이 모델 정의를 위한 고객 입력 폼](#34-게이트웨이-모델-정의를-위한-고객-입력-폼)
  * [3.5 Thing+에 등록된 장비 리스트](#35-thing에-등록된-장비-리스트)
  * [3.6 임베디드 개발 가이드](#36-임베디드-개발-가이드)
  * [3.7 OAuth 개발 가이드](#37-oauth-이용-가이드)
  * [3.8 Portal 사용 가이드](#38-portal웹-페이지-이용-가이드)
  * [3.9 Gateway-Thing+ 등록/연동 가이드](#39-gateway-thing-등록연동-가이드)
  * [3.10 Thing+ API 이용 가이드](#310-thing-api-이용-가이드)
* [4. API 문서](#4-api-문서)
  * [4.1 Test URL](#41-test-url)
  * [4.2 API 버전](#42-api-버전)

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


## 2. 워크플로우
### 2.1 장비 연동 플로우
 - [Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Bkr%5DWorkflow%20for%20hardware%20interlock_v1.3.pdf)

## 2.2 OAuth/앱 연동 플로우
 - [Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Bkr%5Dworkflow%20for%20utilizing%20oauth_v1.2.pdf)

### 2.3 타 IoT 플랫폼 연동 플로우
 - [추후 제공]

## 3. 가이드
### 3.1 센서 타입
[Link](./SensorTypes_kr.md)

### 3.2 센서 타입 정의를 위한 고객 입력 폼
[Download](./Sensor-type-registration-form.xlsx)

### 3.3 Thing+에 등록된 게이트웨이 모델 리스트
[Link](https://rawgit.com/daliworks/thingplus-guide/master/doc/RegisteredGatewayModelList.html)

### 3.4 게이트웨이 모델 정의를 위한 고객 입력 폼
[Download](./Gateway-model-registration-form.xlsx)

### 3.5 Thing+에 등록된 장비 리스트
[Link](https://rawgit.com/daliworks/thingplus-guide/master/doc/RegisteredGatewayDeviceAndSensorList.html)

### 3.6 임베디드 개발 가이드
[Link](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide.md)

### 3.7 OAuth 이용 가이드
[Link](./OAuth2Guide_kr.md)

### 3.8 Portal(웹 페이지) 이용 가이드
[Link](http://support.thingplus.net/ko/user-guide/registration.html#id-enduser)

### 3.9 Gateway-Thing+ 등록/연동 가이드
[Link](./registerGateway_kr.md)

### 3.10 Thing+ API 이용 가이드
[Link](./intro_kr.md)

## 4. API 문서
[Link](https://thingplus.api-docs.io/2.0/)

### 4.1 Test URL
https://www.sandbox.thingplus.net/

### 4.2 상용(정식) Service URL
상용(정식) 서비스를 이용하시기 위해서는 `Thing+`에 요청이 필요합니다. 상용 서비스에 개설을 원하신다면,  contact@thingplus.net 으로 연락을 부탁드립니다.
https://***.thingplus.net/ (*** 는 서비스 고유의 url 입니다)

ex1) https://myiot.thingplus.net/

ex2) https://www.hello.thingplus.net/

> 주의: 개설한 서비스가 속해있는 지역을 확인하세요. 현재 Thing+는 월드와이드(.net), EU지역(.eu)를 지원하고 있습니다.

상용 API 서버 URL:
For thingplus.net services: https://api.thingplus.net/v2
For thingplus.eu services: https://api.thingplus.eu/v2

### 4.3 API Version
Thing+ API의 최신 버전은 v2.0이며 API 문서도 v2.0기준으로 되어 있습니다.


## Changes history

#### 2017.10.10
add `sandbox` url on `oauth2` detail page

add [3.9 Gateway-Thing+ 등록/연동 가이드](#39-gateway-thing-등록연동-가이드)

## License
