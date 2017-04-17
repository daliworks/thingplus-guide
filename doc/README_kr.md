# Thing+ 가이드

## Conents
* [용어 설명](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#용어-설명)
* [장비 연동 플로우](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#장비-연동-플로우)
* [임베디드 가이드](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#임베디드-가이드)
* [oAuth/앱 연동 플로우](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#oauth앱-연동-플로우)
* [oAuth 가이드](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#oauth-가이드)
* [API 문서](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#api-문서)
* [타 IoT 플렛폼 연동 플로우](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#타-iot-플렛폼-연동-플로우)
* [Portal 사용 가이드](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#portal-사용-가이드)
* [Changes history](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#changes-history)
* [License](https://github.com/daliworks/thingplus-guide/blob/master/doc/README_kr.md#license)

### 용어 설명
- Sensor: 특정 값을 수집하거나 상태를 감지하는 HW. 외부로 부터 입력을 받는것은 불가능하고 전송만 가능하다.  (ex: 온도, 습도 센서 등)
- Actuator: 외부 입력을 받아 특정한 동작이 가능한 HW. (ex: LED Actuactor, on/off Actuator)
- Gateway: 서버와 통신을 하는 HW/SW (ex: 센서값을 서버로 전달. 서버로부터 센서로 명령을 전달)   
- Device: 여러개의 센서를 묶는 가상의 단위. 게이트웨이는 1개 이상의 디바이스를 처리 할 수 있음.
- oAuth2 : 권한 인증을 수행할 수 있는 표준 Open Protocol  
  ![oauth](https://github.com/daliworks/thingplus-guide/blob/master/doc/images/oauth2.png "oauth")
- User Type  
  - Servive Admin: 특정 IoT서비스에 대한 관리를 하는 슈퍼 유저.
  - Site Admin: 게이트웨이의 관리(추가, 삭제, 변경)가 가능한 User. 
  - End User: Site admin에게 게이트웨이 또는 센서의 권한을 할당받은 유저. 게이트웨이관리가 불가능.
  
### 장비 연동 플로우
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/[kr]flow_for_hardware_v1.1.pdf)

### 임베디드 가이드
[Link](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide.md)

### oAuth/앱 연동 플로우
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/[kr]flow_for_app_with_oauth2_v1.1.pdf)

### oAuth 가이드


### API 문서
[Link](https://thingplus-10.api-docs.io/2.0/)

### 타 IoT 플렛폼 연동 플로우


### Portal 사용 가이드


### Changes history



### License
