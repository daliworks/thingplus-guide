# Thing+ Guide
Read the glossary and follow the flow to develop.
Even if you do not have equipment yet, we provide a simple simulator.

`SandBox` may have some incomplete features in commercial services and may be temporarily unavailable

Sometime `SandBox` have some incomplete features. `SandBox` Service may be discontinued without notice.
<br>Please contact us for commercial service <contact@thingplus.net>

## Conents
* [1. Glossary](#1-glossary)
* [2. Flow for interworking hardware(embedded)](#2-flow-for-interworking-hardwareembedded)
* [3. embedded Development Guide](#3-embedded-development-guide)
* [4. Flow for interworking oAuth/App](#4-flow-for-interworking-oauthapp)
* [5. oAuth Development Guide](#5-oauth-development-guide)
* [6. API document](#6-api-document)
* [7. Portal Use Guide](#7-portal-use-guide)
* [Flow for interworking another Iot platform](#8-flow-for-interworking-another-iot-platform)

## 1. Glossary

| Term | Description | example
| --- | --- | ----
| Sensor | the hw to collect some value or state<br>Defiend All sensor include Actuator | temperature, humidity
| Actuator | the hw to input command from outside | camera, switch
| Device | Group of Sensor. Sometime the group is virtual but some time is real<br> Gateway have to composed by at least one device |
| Gateway | HW / SW to communicate with server <br> send sensor value/status to server or forward command from server to sensor |
| Tag | Units that can be grouped and managed by existing sensors scattered across multiple devices / gateways |
| oAuth2 | The standard Open Protocol can be performed authorization authentication | 
| Service | Iot Service which offered to customer |
| Site | A management group inside a service or a group of users |
| Admin | An administrator who manages a service or site |
| User | Anyone registered on the site|
| Rule | a feature to automatically execute the function according to specific conditions | When the temperature is less than 10 degrees Boiler turn on


#### 1.1 Additional explanation
1. example about Service/Site
    * Monitor temperature / humidity of each classroom in school IoT
        * Service - the school temperature / humidity management system service
        * Site - each classroom
        * Service Admin - Business managers who provide services
        * Site Admin - Manager who manages the hw in each classroom (ex: teacher or caretaker)
        * User - All Student. Check temperature for each classroom through website / app
    * IoT to measure/analyze electricity usage by apartments
        * Service - Real-time electricity usage service
        * Site - each branch of apartments
        * Service Admin - Business managers who provide services
        * Site Admin - Electrical staff managing the power/usage of electricity by each branch
        * User - Apartment resident. Check your home electricity usage
        
1. example about Gateway/Device/Sensor/Tag
    * Home IoT with RaspberryPi and IoT Starter Kit. Assume that there are two temperature and humidity sensors
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
