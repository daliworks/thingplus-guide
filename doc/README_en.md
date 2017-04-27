# Thing+ Guide
Read the glossary and follow the flow to develop with Thing+.
Even if you do not have equipment yet, we provide a simple virtual gateway and several sensor simulators.

The `SandBox` may have some incomplete features compared with the commercial site and may be temporarily unavailable.

From time to time, the `SandBox` will also have new features that are still in testing. Additionally, the `SandBox` Service may be discontinued without notice, so please keep this in mind when using it.
<br>Please contact us here if you are ready to begin using Thing+ for commercial service - <contact@thingplus.net>

## Contents
* [1. Glossary](#1-glossary)
* [2. Workflow](#2-workflow)
  * [2.1 for hardware interlock with Thing+(embedded)](#21-for-hardware-interlock-with-thingembedded)
  * [2.2 for utilizing OAuth/App](#22-for-utilizing-oauthapp)
  * [2.3 for interlocking with another Iot platform](#23-for-interlocking-with-another-iot-platform)

* [3. Guides](#3-guides)
  * [3.1 Sensor Types](#31-sensor-types)
  * [3.2 Sensor Type Registration Form](#32-sensor-type-registration-form)
  * [3.3 Registered Gateway Model List](#33-registered-gateway-model-list)
  * [3.4 Gateway Model Registration Form](#34-gateway-model-registration-form)
  * [3.5 Registered Gateway, Device and Sensor List](#35-registered-gateway-device-and-sensor-list)
  * [3.6 Embedded Development Guide](#36-embedded-development-guide)
  * [3.7 OAuth Development Guide](#37-oauth-development-guide)
  * [3.8 Portal Usage Guide](#38-portal-usage-guide)

* [4. API documentation](#4--api-documentation)
  * [4.1 Test URL](#41-test-url)
  * [4.2 API Version](#42-api-version)


## 1. Glossary

| Term | Description | example
| --- | --- | ----
| Sensor | A hardware used to collect some value or state | ex) temperature sensor, humidity sensor, etc
| Actuator | A hardware designed to receive a command and perform an action | ex) camera, switch, etc
| Device | A group of Sensors. Sometime the group is virtual but most often is real - this can also be referred to as an "Edge Node", "Node","Sensor Node", or "Sensor Device" <br> Gateways have to include at least one device (in Thing+, not neccessarily physically) |
| Gateway | HW / SW that allows communication with Thing+ servers <br> Sends sensor values/status to the server or forwards commands from the server to sensors/actuators |
| Sensor Type | Refers to a sensor’s classification regarding the physical quantity that it is capable of taking. On a per-sensor type basis, the unit, icon, etc… is usually different, as well as the rules that can be set using that sensor. | ex) temperature, humidity, etc
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
        
2. Example regarding Gateway/Device/Sensor/Tag usage
    * Home IoT with RaspberryPi and an IoT Starter Kit. Assume that there are two temperature and humidity sensors
        * Sensor - temperature sensor, humidity sensor
        * Actuator - Led sensor that can be turned on/off
        * Device - RaspberryPi Starter Kit
        * Gateway - RaspberryPi
        * Tag - temperature sensor 1, humidity sensor 1 both tagged with `Room` (a geo-local tag basically), temperature sensor 2, humidity sensor2 Tagged `Living Room` - though this, easily create rules/actions on a per-room basis

## 2. Workflow

### 2.1 for hardware interlock with Thing+(embedded)
 - [Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Ben%5DWorkflow%20for%20hardware%20interlock_v1.3.pdf)

### 2.2 for utilizing OAuth/App
 - [Download](https://github.com/daliworks/thingplus-guide/raw/master/doc/src/dist/%5Ben%5Dworkflow%20for%20utilizing%20oauth_v1.2.pdf)

### 2.3 for interlocking with another Iot platform
 - [To be provided later]

## 3. Guides

### 3.1 Sensor Types
[Link](./SensorTypes_en.md)

### 3.2 Sensor Type Registration Form
[Download](./Sensor-type-registration-form.xlsx)

### 3.3 Registered Gateway Model List
[Link](https://rawgit.com/daliworks/thingplus-guide/master/doc/RegisteredGatewayModelList.html)

### 3.4 Gateway Model Registration Form
[Download](./Gateway-model-registration-form.xlsx)

### 3.5 Registered Gateway, Device and Sensor List
[Link](https://rawgit.com/daliworks/thingplus-guide/master/doc/RegisteredGatewayDeviceAndSensorList.html)

### 3.6 Embedded Development Guide
[Link](https://github.com/daliworks/thingplus-embedded/blob/master/docs/Thingplus_Embedded_Guide_EN.md)

### 3.7 OAuth Development Guide
[Link](./OAuth2Guide_en.md)

### 3.8 Portal Usage Guide
[Link](http://support.thingplus.net/en/user-guide/registration.html#id-enduser)

## 4.  API documentation
[Link](https://thingplus-22.api-docs.io/2.0)

### 4.1 Test URL
https://nocert.sandbox.thingplus.net/

### 4.2 API Version
The current Thing+ API version and documentation is v2.0.

However, for the time being, only sandbox.thingplus.net is on the v2.0 system.
Other services are currently using v1.0 of the API.

This is temporary, and we intend to update all service locations to v2.0 soon.

## Changes history


## License
