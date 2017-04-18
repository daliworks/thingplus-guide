# Thing+ 가이드

## Conents
* [용어 설명](#용어-설명)
* [장비 연동 플로우](#장비-연동-플로우)
* [임베디드 가이드](#임베디드-가이드)
* [oAuth/앱 연동 플로우](#oauth앱-연동-플로우)
* [oAuth 가이드](#oauth-가이드)
* [API 문서](#api-문서)
* [타 IoT 플렛폼 연동 플로우](#타-iot-플렛폼-연동-플로우)
* [Portal 사용 가이드](#portal-사용-가이드)
* [Changes history](#changes-history)
* [License](#license)

## 1. 용어 설명

| 용어 | 용어 설명 | 예
| --- | --- | ----
| Sensor | 특정 값을 수집/전송/상태를 감지하는 HW. Actuator를 포함한 모든 센서를 Sensor로 정의 | 온도, 습도 센서 등  
| Actuator | 외부 입력을 받아 특정한 동작이 가능한 HW | LED Actuactor, on/off Actuator, Camera Actuator
| Device | 센서의 그룹. 실제 HW일수 있음. 게이트웨이는 최소 1개 이상의 디바이스를 처리 | 
| Gateway | 서버와 통신을 하는 HW/SW. 센서값/상태를 서버로 전달하거나 서버로부터 센서로 명령을 전달 |
| Tag | 여러 디바이스/게이트웨이에 흩어져 존재하는 Sensor를 그룹화하여 관리 할 수 있는 단위 |
| oAuth2 | 권한 인증을 수행할 수 있는 표준 Open Protocol | 
| Service | ddd | aa
| Site | aa | aaa
| 관리자 | ㅁㅁㅁ | 
| 사용자 | ㅁㅁㅁ |
| 규칙 | ㅁㅁㅁ | 

![oauth](https://github.com/daliworks/thingplus-guide/blob/master/doc/images/oauth2.png "oauth") |

User Type  
  - Servive Admin: 특정 IoT서비스에 대한 관리를 하는 슈퍼 유저.
  - Site Admin: 게이트웨이의 관리(추가, 삭제, 변경)가 가능한 User. 
  - End User: Site admin에게 게이트웨이 또는 센서의 권한을 할당받은 유저. 게이트웨이관리가 불가능.
  
## 2. 장비 연동 플로우
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/[kr]flow_for_hardware_v1.1.pdf)

## 3. 임베디드 가이드
[Link](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide.md)

## 4. oAuth/앱 연동 플로우
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/[kr]flow_for_app_with_oauth2_v1.1.pdf)

## 5. oAuth 가이드


## 6. API 문서
[Link](https://thingplus-10.api-docs.io/2.0/)

#### Test

#### Response Status Code
기본적으로 http response status code 동일

#### Thing+ Error Code


## 7. 타 IoT 플렛폼 연동 플로우


## 8. Portal 사용 가이드


## 9. Changes history



## 10. License
