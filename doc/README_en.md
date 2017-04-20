# Thing+ Guide
Read the glossary and follow the flow to develop with Thing+.
Even if you do not have equipment yet, we provide a simple virtual gateway and several sensor simulators.

The `SandBox` may have some incomplete features compared with the commercial site and may be temporarily unavailable.

From time to time, the `SandBox` will also have new features that are still in testing. Additionally, the `SandBox` Service may be discontinued without notice, so please keep this in mind when using it.
<br>Please contact us here if you are ready to begin using Thing+ for commercial service - <contact@thingplus.net>

## Conents
* [1. Glossary](#1-glossary)
* [2. Workflow for hardware interlock with Thing+(embedded)](#2-workflow-for-hardware-interlock-with-thingembedded)
* [3. Embedded Development Guide](#3-embedded-development-guide)
* [4. Workflow for utilizing OAuth/App](#4-workflow-for-utilizing-oauthapp)
* [5. OAuth Development Guide](#5-oauth-development-guide)
* [6. API documentation](#6--api-documentation)
* [7. Portal Usage Guide](#7-portal-usage-guide)
* [8. Flow for interlocking with another Iot platform](#8-flow-for-interlocking-with-another-iot-platform)

## 1. Glossary

| Term | Description | example
| --- | --- | ----
| Sensor | hardware used to collect some value or state<br> | ex) temperature, humidity
| Actuator | hardware designed to receive a command and perform an action | ex) camera, switch
| Device | A group of Sensors. Sometime the group is virtual but most often is real - this can also be referred to as an "Edge Node", "Node","Sensor Node", or "Sensor Device" <br> Gateways have to include at least one device (in Thing+, not neccessarily physically) |
| Gateway | HW / SW that allows communication with Thing+ servers <br> Sends sensor values/status to the server or forwards commands from the server to sensors/actuators |
| Tag | "Tags" are identifiers used to group and manage sensors/actuators scattered across multiple devices / gateways |
| OAuth2 | A standard Open Protocol that can be used to perform authorization and authentication on Thing+ |
| Service | A "Service" is the highest organizational level offered to customers and includes complete administration functions (dashboard locking, sensor selection, etc..). A service can include many "Sites", and in those sites, many gateways, users, sensors, etc.. |
| Site | A division inside of a service designed to allow for management of specific groups of users, devices, etc.. - Site's can have their own administrators. <br> ex) A hospital may be a single "site", or may be divided into multiple sites, each designed to represent a specific physical location, or a specific user group. |
| Admin | An administrator who manages a service or site |
| User | Anyone registered directly to a site are "users"|
| Rule | A feature to automatically execute a function/action according to specific conditions and triggers | ex) When the temperature is less than 10 degrees, send a command signal to the boiler actuator


#### 1.1 Additional explanation
1. Service/Site example
    * Monitor temperature / humidity of each classroom in a school's IoT solution
        * Service - represent the school's entire Thing+ related temperature / humidity management system
        * Site - includes all of the users, devices, and gateways for each classroom
        * Service Admin - Business manager and/or IT manager
        * Site Admin - Manager who manages the hw in each classroom (ex: teacher or caretaker)
        * User - All Students. Can check temperatures for each classroom through PC/Smartphone/etc..
    * IoT solution to measure/analyze electricity usage by apartments
        * Service - Real-time electricity usage across a city's apartments
        * Site - each single apartment complex
        * Service Admin - City-wide apartment director/manager
        * Site Admin - Electrical staff managing the power/usage of electricity of each apartment complex
        * User - Apartment residents. May check their home electricity usage
        
1b. Example regarding Gateway/Device/Sensor/Tag usage
    * Home IoT with RaspberryPi and an IoT Starter Kit. Assume that there are two temperature and humidity sensors
        * Sensor - temperature sensor, humidity sensor
        * Actuator - Led sensor that can be turned on/off
        * Device - RaspberryPi Starter Kit
        * Gateway - RaspberryPi
        * Tag - temperature sensor 1, humidity sensor 1 both tagged with `Room` (a geo-local tag basically), temperature sensor 2, humidity sensor2 Tagged `Living Room` - though this, easily create rules/actions on a per-room basis


## 2. Workflow for hardware interlock with Thing+(embedded)
[Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Ben%5DWorkflow%20for%20hardware%20interlock_v1.3.pdf)

## 3. Embedded Development Guide
[Link](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide_EN.md)

## 4. Workflow for utilizing OAuth/App
 [Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Ben%5Dworkflow%20for%20utilizing%20oauth_v1.2.pdf)

## 5. OAuth Development Guide
[Link](./OAuth2Guide_en.md)

## 6.  API documentation
[Link](https://thingplus-10.api-docs.io/2.0/)

#### 6.1 Test URL
https://nocert.sandbox.thingplus.net/

#### 6.2 Response Status Codes
The http response status code is the same as here.

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


#### 6.3 API Error Codes
Thing+ API Error Categories & Codes are `strings`

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
| GATEWAY_ERROR | PROCESS_COMMAND_RESULT | unknown error when receiving result from gateway
| UNKNOWN | - |



## 7. Portal Usage Guide
[Link](http://support.thingplus.net/en/user-guide/registration.html#id-enduser)

## 8. Flow for interlocking with another Iot platform
[To be provided later]

## Changes history


## License
