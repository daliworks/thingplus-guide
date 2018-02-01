# Thing+ OAuth2 Authorization Scopes
Thing+ OAuth2 Authorization Scopes 는 Authorization Code Grant 을 사용하여 Thing+ OAuth2 AccessToken 을 획득할 때 Thing+ OAuth2 AccessToken에 액세스 권한을 부여합니다. 액세스 부여 권한은 사용자 계정에 부여된 권한을 넘어설 수 없습니다. Scopes 는 User, Gateway, Timeline, Tag, Rule, Service, Site, Billing 에 대한 액세스 권한을 부여할 수 있으며 권한을 넘어서서 사용자 리소스에 접근 할 경우 액세스가 거부됩니다.

권장되는 기본 Scopes 는 **user-profile-read, gateway-update, timeline-read, tag, rule-read, service-read** 입니다. 만약 사용자 계정에 부여된 권한을 넘어선 추가 권한을 부여할 필요가 있으신 경우 contact@thingplus.net 로 요청하시기 바랍니다.

Authorization Code Grant 방식을 사용할 때 authorize scopes 에 아래 scope 접근 권한을 부여하면 됩니다.

## Authorization Scopes

**권장되는 기본 Scopes 를 사용하는 것을 추천합니다.**

스코프(Scope) - Thing+ authClients API 을 호출하여 **Thing+ OAuth2 client 등록시 scopes 에 넣어 줄 수 있는 옵션**입니다. 스코프(Scope)를 이용해서 사용가능한 API 범위를 개발자가 지정할 수 있습니다.

리소스(API) - 해당 스코프(Scope)가 지정하는 **사용가능한 API** 입니다. [각 API 에 대한 자세한 설명은 이 문서를 참조하십시오.](https://thingplus.api-docs.io)

| 스코프(Scope) | 리소스(API) | 설명
| - | - | -
| (No scope)         | (No API.)| 어떤 scopes 도 액세스 할 수 없습니다.
| user-profile       | users/me, /changePassword | (TBD) **사용자 프로필 읽기**와 **업데이트 권한**을 지정합니다.
| user-profile-read  | users/me | 사용자 프로필 읽기 권한을 지정합니다.
| gateway            | /gateways, /registerGateway, /registerGatewayKey, /manageGateway, /controlActuator, /sensorTypes, /sensorDrivers, /gatewayModels | (TBD) **사용자의 게이트웨이, 디바이스, 센서, 컨트롤 액츄에이터**에 대해 **등록, 읽기, 업데이트, 삭제 권한**을 지정합니다.
| gateway-read       | /gateways, /controlActuator | **사용자의 게이트웨이, 센서, 컨트롤 액츄에이터**에 대해 **읽기 권한**을 지정합니다.
| gateway-update     | /gateways, /manageGateway,  /controlActuator | 사용자의 **게이트웨이 관리 권한**을 포함하여 **게이트웨이, 디바이스, 센서, 컨트롤 액츄에이터**에 대해 **읽기, 업데이트 권한**을 지정합니다.
| timeline-read      | /timelines | **사용자의 타임라인 읽기 권한**을 지정합니다.
| tag                | /tags | **사용자의 태그**에 대해 **생성, 읽기, 업데이트, 삭제 권한**을 지정합니다.
| tag-read           | /tags | **사용자의 태그**에 대해 **읽기 권한**을 지정합니다.
| rule               | /rules, /pushDevices | (TBD) **사용자의 규칙**에 대해 **읽기, 업데이트, 삭제 권한**을 지정합니다.
| rule-read          | /rules | **사용자의 규칙**에 대해 **읽기 권한**을 지정합니다.
| service-read       | /services | **사용자가 등록 되어있는 서비스**에 대해 **읽기 권한**을 지정합니다.
| site-read          | /site | **사용자가 등록한 사이트**에 대해 **읽기 권한**을 지정합니다.
| billing-read       | /billings | (TBD) **사용자의 청구 정보**에 대해 **읽기 권한**을 지정합니다.

**TBD** : 현재 사용가능하지 않음
