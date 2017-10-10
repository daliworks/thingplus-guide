# Thing+ 게이트웨이 등록 가이드

Thing+ IoT는 게이트웨이 / 센서와 함께 시작합니다.

센서가 측정한 값을 서버로 전송하기 위해서는 `게이트웨이`가 필수적이며 각 용어에 대한 설명은 [여기](./README_kr.md#1-%EC%9A%A9%EC%96%B4-%EC%84%A4%EB%AA%85)에서 확인 가능합니다.

Thing+ IoT 서비스를 이용하기 위해 아래 내용이 필요합니다

1. `게이트웨이`와 `Thing+ Server`간의 연동
 - 게이트웨이에서 정보를 서버로 전달하는 과정입니다
 - 게이트웨이와 Thing+ Server간 통신에 필요한 인증은 `APIKEY` 를 이용합니다.
 - `APIKEY`를 획득하는 과정은 [여기](#1-APIKEY-생성)를 참조하시기 바랍니다.
 - `게이트웨이`와 `Thing+ Server`의 연동의 자세한 내용은 [여기](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide.md)를 참조하시기 바랍니다.
2. 사용자에게 `게이트웨이` 등록
 - 특정 사용자가 해당 게이트웨이를 등록/획득 하는 과정입니다
 - `Thing+ Server`와 연동된 `게이트웨이`와 `센서`에 대한 정보를 조회 하기 위해 반드시 필요한 절차입니다.


## 1. APIKEY 생성
게이트웨이와 Thing+ Server간 통신에 필요한 Key인 `APIKEY`를 생성하는 방법은 두가지가 있습니다.

1. `APIKEY`를 생성후 게이트웨이에 전달하는 방법
2. 게이트웨이가 직접 `APIKEY`를 획득 하는 방법
 - 해당 기능을 위해서는 vendorKey가 필요하며 Thing+에 vendorKey 요청이 필요합니다.

해당 방법은 게이트웨이나 개발환경에 따라 차이가 있습니다.


### 1.1 APIKEY 생성 후 전달

#### Thing+ Portal(웹 페이지) 에서 획득

1. 사용하려는 게이트웨이의 model과 고유 ID를 입력하여 `APIKEY` 생성 [영상보기]()

#### Thing+ API를 통한 획득

1. registerGatewayKey API의 1번 ```authType = apikey ``` 사용 [API 가이드](https://thingplus.api-docs.io/2.0/non-rest-apis/registergatewaykey)

생성한 APIKEY를 게이트웨이 코드에 입력하거나 다른 방법을 통해 전달

### 1.2 게이트웨이가 APIKEY를 획득

주의: 해당 기능을 위해서는 vendorKey가 필요하며 Thing+에 vendorKey 요청이 필요합니다.

#### Thing+ Portal(웹 페이지) 에서 APIKEY 획득 가능상태로 변경

1. 사용하려는 게이트웨이의 model과 고유 ID를 입력하여 API 키 활성화 상태로 만듬 [영상보기]()
2. 게이트웨이에서 activateGatewayKey API를 사용하여 APIKEY 획득 [API 가이드](https://thingplus.api-docs.io/2.0/non-rest-apis/activategatewaykey)

#### Thing+ API를 통한 획득

1. registerGatewayKey API에서 3번 ```authType = apikeyReady ``` 사용 [API 가이드](https://thingplus.api-docs.io/2.0/non-rest-apis/registergatewaykey)
2. 게이트웨이에서 activateGatewayKey API를 사용하여 APIKEY 획득 [API 가이드](https://thingplus.api-docs.io/2.0/non-rest-apis/activategatewaykey)


## 2. 게이트웨이 등록
서버와 통신에 성공한 게이트웨이 정보를 사용자가 보기 위해서는 게이트웨이 등록이 반드시 필요합니다.

#### Thing+ Portal(웹 페이지) 에서 등록
1. 게이트웨이 등록 화면으로 이동. [영상보기]()
2. 사용하려는 게이트웨이를 선택하고 등록 [영상보기]()


#### Thing+ API를 통한 등록
1. registerGateway API 를 사용 [API 가이드](https://thingplus.api-docs.io/2.0/non-rest-apis/registergateway)
2. [상세 설명](https://github.com/daliworks/thingplus-guide/blob/master/doc/GettingStartedWithHttpsAndOauth.md#5-gateway-등록)
