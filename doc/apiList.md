# Thing+ API List
서버사이드 렌더링을 위한 `view` API 를 제외한 모든 API의 주소는 `{서비스 url}/api/***` 형태를 따름

## 로그인 / 회원가입

method | name | desc
-----------|------ | -----
post | login |
post | sendVerification | 이메일 인증
post | register | 유저 등록
post | resetPassword |
post | setPassword |
post | logout |
post | validate | 유저 가입을 위한 validation
post | validateService | 서비스 신규 등록을 위한 validation
get | signupMethod | 서비스에 회원 새로 가입 될때 방식.
## 서버사이드 렌더링 - 1
서버사이드 렌더링을 위한 API는 URL 에 `/api/` 대신 `/views/` 를 이용.
아래

method | name | desc
-----------|------ | -----
get | views/activate |
get | views/verify |
post | views/emailVerified |
post | views/activated |

## 서버사이드 렌더링 - 2
method | name | desc
-----------|------ | -----
get | views/login |
get | views/resetPassword |
get | views/setPassword |
get | views/verifyEmail |
get | views/userVerifyEmail |
get | views/userRegister |
get | views/aboutTerm |
get | views/registerComplete |

## oAuth 관련 API
  
method | name | desc
-----------|------ | -----
get | oauth2/authorize |
post | oauth2/token |
post | oauth2/authorize/decision|
    

## REST API - Login 불필요
method | name | desc
-----------|------ | -----
get | sensorTypes |
get | sensorTypes/:id |
get | sensorDrivers |
get | sensorDrivers/:id |
get | gatewayModels |
get | gatewayModels/:id |
get | ruleAgents |
get | ruleAgents/:id |
post | activateGatewayKey | 게이트웨이의 APIKEY가 동작하도록 변경 (활성화)

## REST API - Login 필요
method | name | desc
-----------|------ | -----
get | users/me |
put | users/me |
post | users/me/mobile |
put | users/me/mobile |
get | users |
get | users/:id |
put | users/:id |
get | users/:id/:config |
put | users/:id/:config |
get | gateways |
get | gateways/:id |
put | gateways/:id |
del | gateways/:id |
get | gateways/:id/status |
put | gateways/:id/status |
get | gateways/:owner/devices |
post | gateways/:owner/devices |
get | gateways/:owner/devices/:id |
put | gateways/:owner/devices/:id |
del | gateways/:owner/devices/:id |
get | gateways/:owner/sensors |
post | gateways/:owner/sensors |
get | gateways/:owner/sensors/:id |
put | gateways/:owner/sensors/:id |
del | gateways/:owner/sensors/:id |
get | gateways/:owner/sensors/:id/status |
put | gateways/:owner/sensors/:id/status |
get | gateways/:owner/sensors/:id/series |
put | gateways/:owner/sensors/:id/series |
get | roles |
get | roles/:id |
put | roles/:id |
get | services |
post | services|
get | services/:id|
put | services/:id|
del | services/:id|
get | services/:id/:config |
put | services/:id/:config|
get | sites |
post | sites|
get | sites/:id|
put | sites/:id |
del | sites/:id |
post | sensorTypes |
put | sensorTypes/:id |
del | sensorTypes/:id |
post | sensorDrivers |
put | sensorDrivers/:id |
del | sensorDrivers/:id |
post | gatewayModels |
put | gatewayModels/:id |
del | gatewayModels/:id |
get | dafuncs | 통계 예측 관련, 자세히 모르겠음
post | dafuncs |
get | dafuncs/:id |
put | dafuncs/:id |
del | dafuncs/:id |
get | statsfuncs | 통계 지원 가능 목록 및 파라미터 정보
post | statsfuncs |
get | statsfuncs/:id |
put | statsfuncs/:id|
del | statsfuncs/:id |
get | timelines |
post | timelines |
get | timelines/:id |
put | timelines/:id |
del | timelines/:id |
get | rules |
post | rules|
get | rules/:id|
put | rules/:id|
del | rules/:id|
get | tags|
post | tags|
get | tags/:id|
put | tags/:id|
del | tags/:id|
get | labels|
post | labels|
get | labels/:id|
put | labels/:id|
del | labels/:id|
get | labelsCombi/:ids| 교집합해서 가져오는것 - 일희피디님 문의 필요
get | comments |
post | comments|
get | comments/:id|
put | comments/:id|
del | comments/:id|
get | comments/:id/replies|
post | comments/:id/replies|
put | comments/:id/replies/:rid|
post | staticFiles| 일종의 service 별 config info object
get | staticFiles/:file|
put | staticFiles/:file|
del | staticFiles/:file|
get | damodels|
post | damodels| 알수없음
get | damodels/:id|
put | damodels/:id|
del | damodels/:id|
get | widgetTypes|
post | widgetTypes|
get | widgetTypes/:id|
put | widgetTypes/:id|
del | widgetTypes/:id|
get | dashboardTemplates| dashboard에서 사용 가능한 widget Types. TODO move to config
post | dashboardTemplates|
get | dashboardTemplates/:id|
put | dashboardTemplates/:id|
del | dashboardTemplates/:id|
get | dashboards|
post | dashboards|
get | dashboards/:id|
put | dashboards/:id|
del | dashboards/:id|
get | widgets|
post | widgets|
get | widgets/:id|
put | widgets/:id|
del | widgets/:id|
get | indoorMaps|
post | indoorMaps|
get | indoorMaps/:id|
put | indoorMaps/:id|
del | indoorMaps/:id|
get | pushDevices| native push
post | pushDevices|
get | pushDevices/:id|
put | pushDevices/:id|
del | pushDevices/:id|
get | authClients|
post | authClients|
get | authClients/:id|
del | authClients/:id|
get | authScopes|
get | authScopes/:id|
get | billingCharges |
get | billingTargets/:group|
put | billings/site/:id|
put | billings/user/:id|
get | billings|
get | billings/:mtype|
get | paymentAgents|
get | paymentAgents/:id|
get | payments|
post | payments|
get | payments/:id|
put | payments/:id|
del | payments/:id|
get | paymentTransactions|
get | paymentTransactions/:id |
get | getPaymentTransactions|
get | agreedPreApproval|
get | canceledPreApproval|
get | coupons| 현재 안씀
get | coupons/:id|
put | coupons/:id|
del | coupons/:id|
get | vendors| activateKey를 위해 필요
get | vendors/:id|
put | vendors/:id|
del | vendors/:id|
get | gatewayWhitelists|
post | gatewayWhitelists|
post | gatewayWhitelists/bulk|
get | gatewayWhitelists/:id|
put | gatewayWhitelists/:id|
del | gatewayWhitelists/:id|
get | extChannels| slack or another messanger
post | extChannels|
get | extChannels/:id|
put | extChannels/:id|
del | extChannels/:id|
get | extIntegrations|
post | extIntegrations| slack 연동 key 저장
get | extIntegrations/:id|
put | extIntegrations/:id|
del | extIntegrations/:id|
get | reports|
post | reports|
get | reports/:id|
put | reports/:id|
del | reports/:id|
get | reportItemTypes|
get | things|
post | things|
get | things/:id|
put | things/:id|
del | things/:id|
get | thingTree/:id|
get | thingTypes|
post | thingTypes|
get | thingTypes/:id|
put | thingTypes/:id|
del | thingTypes/:id|
get | ext/slack/app/redirect| slack 연동시 이용
get | ext/slack/data/get| slack 연동시 이용
      

## None REST API
method | name | desc
-----------|------ | -----
post | manageUser|
post | manageSite|
post | generateInviteCode|
post | changePassword|
post | registerGatewayKey|
get | getAPIKey|
post | registerGateway|
post | manageGateway|
post | loadSeries| add sensor series data by bulk
post | activateChannel| 트위터 관련 코드 (사용안함)
post | controlActuator|

                                     
## Internal 관리자 API
method | name | desc
-----------|------ | -----
post | internal/initialData|
post | internal/migrationData| deprecated
post | internal/preregisterGateways| systemAdmin이 타유저의 게이트웨이를 미리 등록.
post | internal/updateAllRoles|
post | internal/registerVendor| 위의 vendor post
del | internal/users/:id|  알수없음
get | internal/sensors| 게이트웨이를 알수 없는 sensor 획득
get | internal/sensors/:id|
get | internal/mqttClientConnInfos| gateway가 어디 mosca에 붙어있는지. 상태가 어떤지 확인
get | internal/mqttClientConnInfos/:id|
del | internal/mqttClientConnInfos/:id|
get | internal/serverLogs| 여러 서버의 error 로그들을 획
get | internal/serverLogs/:id|
post | internal/delAllLocalStrategySession/service/:id| 서비스 이용자 전체 강제 세션 아웃
post | internal/delAllLocalStrategySession/user/:id| 특정 이용자 세션아웃
post | internal/manageRateLimiters| limiter 관련 제어 (controlActuator )
get | admin/query| admin이 특정 db get
put | admin/querySave| admin이 특정 db put
post | admin/es| Elastic Search 에 query