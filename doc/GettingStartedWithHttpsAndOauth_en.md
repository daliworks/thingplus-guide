# Thing + Interworking Guide with HTTPS and OAuth2 - ENGLISH
## Contents
1. [Overview](#1-Overview)
2. [Preparation](#2-Preparations)
3. [Create OAuth Client](#3-oauth-client-generated)
4. [Access Token Acquisition](#4-access-token-Acquisition)
5. [Gateway registration](#5-gateway-registration)
6. [Device Registration](#6-device-registration)
7. [Sensor Registration](#7-sensor-registration)
8. [Status transmission](#8-status-transmission)
9. [Sensor value transfer](#9-sensor-value-transfer)

## 1. Overview
This document describes how to register gateways and sensors and send sensor values using the privileges of a user who can register the gateway, such as a service administrator or site administrator.

* Common gateway uses API key but it is not appropriate to apply the API key every time using the Thing+ Portal. It is applied when server or native app that can handle personal information such as user ID is linked with Thing+.
* Obtain authority using OAuth2, and register and transfer data and values using HTTPS.
* Actuators can not be linked using this method.
* If the account of the user who provided the privilege at the time of registration is deleted from Thing +, the privileges will disappear and your code will stop working.
* Acquired privileges are retained for 90 days, so you will need to reissue your access token when your due date expires.

## Preparation
* Requires a tool that can call the HTTPS API to call the OAuth Client enrollment API.

    - [Google Chrome](https://www.google.com/chrome/browser/desktop): Use this to sign in to Thing+ Portal.
    
    - [Postman](https://www.google.co.kr/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&ved=0ahUKEwjPiOf6mfvTAhXEJ5QKHbnBBZsQFggoMAI&url=https%3A%2F%2Fchrome.google.com%2Fwebstore%2Fdetail%2Fpostman%2Ffhbjgbiflinjbdggehcddcbncdddomop%3Fhl%3Den&usg=AFQjCNE_Yq59TT1ZExzJ68FTldg4ho_lGw&cad=rjt): This is the Google Chrome App you can use to call the desired HTTPS API.
    
    - [Postman Interceptor](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&sqi=2&ved=0ahUKEwj8p8etmvvTAhVDv5QKHZDDCP8QFgggMAMA&url=https%3A%2F%2Fchrome.Google.com%2Fwebstore%2Fdetail%2Fpostman-interceptor%2Faicmkgpgakddgnaphhhpliifpcfhicfo%3Fhl%3Den&usg=AFQjCNEuLccEMU2awxCgNKPUPhTk4AKv0w): A Google Chrome extension that allows Postman to share cookies created when logged in to the Thing+ Portal.
    
    - Even if you do not use the above tool, you can still do so by using a tool that allows you to call the HTTPS POST API while logged in from the Thing+ Portal.
    
    - [Thing + Support site](http://support.thingplus.net/en/rest-api/getting-started.html#id-step1).
    
    - For more information about the APIs used, see [Thing + API Reference](https://thingplus.api-docs.io/2.0).

## Creating OAuth Client

1. On `Chrome`, go to Thing + Portal and log in with your service administrator account.

2. Execute `Postman`, On Postman Intercepter, and then call the following API.

    - URL: https://api.sandbox.thingplus.net/v2/authClients
    
    - Method: POST
    
    - Content-Type: application / json
    
    - Body:
    
        - Example
          ```json
          {
            "name": "Test Client for Daliworks",
            "reqId": "testClientId",
            "clientSecret": "testClientPwd12!@",
            "scopes": ["gateway", "site-read"]
          }
          ```
        - name: auth You can freely enter the name of the client.
        - reqId: auth The ID of the client to be used to obtain the access token. Enter the value you have set.
        - clientSecret: auth This is used to get the access token from the client's secret value. Enter the value you have set.
        - scopes: Lists the permissions to grant to the auth client. See [link] (https://github.com/daliworks/thingplus-guide/blob/master/doc/OAuth2.md#scopes) for the values ​​you can enter in scopes.

    - Response
        - Example

          ```Json
          {
            "StatusCode": 201,
            "Message": "Created",
            "Data": {
              "Name": "Test Client for Daliworks",
              "ClientSecret": "testClientPwd12! @",
              "Scopes": [
                "Gateway",
                "Site-read"
              ],
              "_user": "1",
              & Quot; mtime & quot ;: 1495422902432,
              "Ctime": 1495422902432,
              "Id": "testClient"
            }
          }
          ```

## Access Token acquisition
1. Obtain an access token from the application using the following APIs:
    - URL: https://api.sandbox.thingplus.net/v2/oauth2/token
    - Method: POST
    - Body:
        - Example

          ```Json
          {
            "Grant_type": "password",
            "Client_id": "testClient",
            "Client_secret": "testClientPwd12! @",
            "Username": "serviceadmin",
            "Password": "0b54b2a7b72f1efeb2c86885c3247787"
          }
          ```
        - grant_type: Enter the string "password" as it is. (** This should not be your user password, please be careful.)
        - client_id: Enter the ID value of the auth client generated by the / v2 / authClient API.
        - clientSecret: Enter the secret value of the auth client generated by the / v2 / authClient API.
        - username: Enter the ID of the user (usually the service administrator) who logged in to Thing + Portal when creating the auth client.
        - password: Enter the md5 hash value of the user password that was logged into Thing + Portal when creating the auth client.
            - On OSX or Linux, use the following command to get the md5 hash value.
                - OSX

                  <Pre>
                  $ Echo -n <b> your_password </ b> | Md5
                  0b54b2a7b72f1efeb2c86885c3247787
                 </ Pre>
                 
               - Linux
               
                  <Pre>
                  $ Echo -n <b> your_password </ b> | Md5sum
                  0b54b2a7b72f1efeb2c86885c3247787 -
                 </ Pre>
               
            - In the environment where the above command does not work, you can get the md5 hash value of the password by using the md5 hash generator on the Internet, but be careful about security.
            - [JavsScript-MD5] (https://github.com/blueimp/JavaScript-MD5) is also available.

- Response
        - Example

          ```Json
          {
            "Access_token": "2yJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiIxIiwiY2xpZW50SWQiOiJ0ZXN0Q2xpZW50SWQiLCJpYXQiOjE0OTU0MzYwMzksImV4cCI6MTUwMzIxMjAzOX0.dQ65zRCgRml96fTc8CDnExAukrFPSLd7NzDlUkf4eYk",
            "Token_type": "Bearer"
          }
          ```
2. Use the acquired access token in the following way when calling the API.
    - Add an `Authorization` field to the Header and a value of` token_type` and `access_token` in a single space.
    - curl example

       ```Bash
       $ Curl -H "Authorization: Bearer 2yJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiIxIiwiY2xpZW50SWQiOiJ0ZXN0Q2xpZW50SWQiLCJpYXQiOjE0OTU0MzYwMzksImV4cCI6MTUwMzIxMjAzOX0.dQ65zRCgRml96fTc8CDnExAukrFPSLd7NzDlUkf4eYk" https://api.sandbox.thingplus.net/v2/gateways
       ```

## Register Gateway
1. Obtaining a Site ID
    - URL: https://api.sandbox.thingplus.net/v2/sites
    - Method: GET
    - Response:
        - Example

          ```Json
          {
             "StatusCode": 200,
             "Message": "OK",
             "Data": [
               {
                 "Billing": "site: 1",
                 "Code": "iService",
                 "Ctime": "1431416762406",
                 "_service": "1",
                 "BillingReserve": "site: 1: reserve",
                 "BillingLimit": "site: 1: limit",
                 "Name": "default",
                 "Id": "1",
                 "BillingMeter": "site: 1: meter",
                 "Mtime": "1431416762406",
                 "BillingCurrent": "site: 1: current"
               }
             ]
          }
          ```
    - A list of sites is returned in the `data` of the response. (Usually 1, but if you create multiple sites, multiple site data will be returned.)
    - Apply the ID of the site you want to register the gateway to the gateway registration API. (In the example, `" id ":" 1"` is the field corresponding to site ID.)

2. Obtaining the Gateway Model ID
    - URL: https://api.sandbox.thingplus.net/v2/gatewayModels/52
    - Method: GET
    - Response:
        - Example

          ```Json
          {
             "StatusCode": 200,
             "Message": "OK",
             "Data": {
               "ReportInterval": "300000",
               "DisplayName": "Open API Gateway",
               "Id": "52",
               "Model": "open-api-gateway-v1.0",
               "DeviceModels": [
                 {
                   "Id": "open-api-device-v1.0",
                   "DisplayName": "Open API Device",
                   "IdTemplate": "{gatewayId} - {deviceAddress}",
                   "Discoverable": "y",
                   "Sensors": [
                     {
                       "Network": "daliworks",
                       "DriverName": "openApiSensor",
                       "Model": "openApiTemp",
                       "Type": "temperature",
                       "Category": "sensor"
                     },
                     {
                       "Network": "daliworks",
                       "DriverName": "openApiSensor",
                       "Model": "openApiHumi"
                       "Type": "humidity",
                       "Category": "sensor"
                     },
     
                     ...
    
                     {
                       "Network": "daliworks",
                       "DriverName": "openApiSensor",
                       "Model": "openApiConductivity",
                       "Type": "conductivity",
                       "Category": "sensor"
                     }
                   ],
                   "Max": 99
                 }
               ],
               "GatewayIdConfig": "n",
               "Mtime": "1495609234518",
               "IdFormat": "uuid",
               "Vendor": "OPEN API",
               "Ctime": "1495609234518",
               "DeviceMgmt": {
                 "ReportInterval": {
                   "Show": "y",
                   "Change": "y"
                 },
                 "DM": {
                   "Poweroff": {
                     "Support": "n"
                   },
                   "Reboot": {
                     "Support": "n"
                   },
                   "Restart": {
                     "Support": "n"
                   },
                   "SwUpdate": {
                     "Support": "n"
                   },
                   "SwInfo": {
                     "Support": "n"
                   }
                 }
               }
             }
          }
          ```
    - The gateway model defines the characteristics of the gateway to be registered. What type of gateway ID to use, what devices and sensors to register, and so on.
    - To register the gateway using the method described in this document, use the gateway model ID `52` (Open API Gateway). If you use a different gateway model, you can substitute `52` in the URL when calling this API by substituting another ID.

3. Creating a Gateway ID
    - For `Open API Gateway`, UUID is used as gateway ID.
    - Obtain the UUID to be used for the ID of the newly registered gateway.
        - In case of OSX, it can be generated with `uuidgen` command.
        - In case of Linux (Ubuntu), `uuid` package can be created by installing` uuid` command after installation.
        - UUID can be obtained in various ways besides this method.
    - Remove the `-` from the UUID obtained above, and change it to lowercase if there is a large block to use as the gateway ID.

       ```Bash
       $ Uuidgen | Tr -d - | Tr [: upper:] [: lower:]
       366d685f93f5477a8d29e8c45bae0a31
       ```

4. Registering the Gateway
    - URL: https://api.sandbox.thingplus.net/v2/registerGateway
    - Method: POST
    - Body:
        - Example

          ```Json
          {
            "Id": "87cd2a6e407511e7922eb724f8803770",
            "Params": {
              "SiteId": "1",
              "Model": "52",
              "Name": "Open Gateway 1"
            }
          }
          ```
        - id: Uses the ID generated by the UUID.
        - siteId: use the site ID obtained above.
        - model: Use the gateway model ID obtained above.
        - name: You can input it freely in the name of the gateway.
        - For options other than those specified, see [Thing + API Reference] (https://thingplus.api-docs.io/2.0/non-rest-apis/registergateway).

    - Response
        - Example

          ```Json
          {
            "StatusCode": 201,
            "Message": "Created",
            "Data": {
              "Name": "Open Gateway 1",
              "Model": "52",
              "_site": "1",
              "_service": "1",
              "ReportInterval": "300000",
              "Mtime": 1495626410619,
              "Ctime": 1495626410619,
              "Tree": "87cd2a6e407511e7922eb724f8803770",
              "Id": "87cd2a6e407511e7922eb724f8803770"
            }
          }
          ```
        - reportInterval: This is the `transmission period`, which is the period (msec) at which the gateway transmits the measured value from the sensor to Thing +. This value can be modified in Thing + Portal 's gateway management.


## Device registration
1. Registration of Device
    - URL: https://api.sandbox.thingplus.net/v2/gateways/{owner}/devices
        - {owner}: Enter the ID of the gateway to which the device is connected. Use the gateway ID registered above.
    - Method: POST
    - Body:
        - Example

          ```Json
          {
             "ReqId": "366d685f93f5477a8d29e8c45bae0a31",
             "Name": "Open Gateway Device 1",
             "Model": "open-api-device-v1.0"
          }
          ```
        - reqId: Creates and uses device ID using UUID.
        - name: You can freely input the name of the device.
        - model: Uses the device model ID in `deviceModels` when querying the gateway model. To register a device using the method described in this document, use the device model ID `open-api-device-v1.0`. If another device model is registered in the gateway model, you can substitute another device model ID when calling this API.
        - See [Thing + API Reference] (https://thingplus.api-docs.io/2.0/gateway-devices/create-gateway-devices) for options other than those specified.

- Response
        - Example

          ```Json
          {
            "StatusCode": 201,
            "Message": "Created",
            "Data": {
              "Name": "Open Gateway 1",
              "Model": "52",
              "_site": "1",
              "_service": "1",
              "ReportInterval": "300000",
              "Mtime": 1495626410619,
              "Ctime": 1495626410619,
              "Tree": "87cd2a6e407511e7922eb724f8803770",
              "Id": "87cd2a6e407511e7922eb724f8803770"
            }
          }
          ```

## 7. Sensor Registration
1. Registering the Sensor
    - URL: https://api.sandbox.thingplus.net/v2/gateways/{owner}/sensors
        - {owner}: Enter the ID of the gateway to which the sensor is connected. Use the gateway ID registered above.
    - Method: POST
    - Body:
        - Example

          ```Json
          {
            "ReqId": "d815ba2f84eb490b8e68d9dd744da397",
            "Name": "Temperature sensor",
            "Type": "temperature",
            "DriverName": "openApiSensor",
            "Model": "openApiTemp",
            "Category": "sensor",
            "DeviceId": "366d685f93f5477a8d29e8c45bae0a31"
          }
          ```
        - reqId: Generate sensor ID using UUID and use it.
        - name: You can freely input the name of the device.
        - model: Uses the device model ID in `deviceModels` when querying the gateway model. To register a device using the method described in this document, use the device model ID `open-api-device-v1.0`. If another device model is registered in the gateway model, you can substitute another device model ID when calling this API.
        - Type in the string: category: `sensor`. Currently, `actuator` is not supported in HTTPS mode.
        - deviceId: Enter the device ID to which the sensor is connected.
        - For options other than those specified, see [Thing + API Reference] (https://thingplus.api-docs.io/2.0/gateway-sensors/create-gateway-sensors).

    - Response
        - Example

          ```Json
          {
            "StatusCode": 201,
            "Message": "Created",
            "Data": {
              "Name": "Temperature sensor",
              "Type": "temperature",
              "DriverName": "openApiSensor",
              "Model": "openApiTemp",
              "Category": "sensor",
              "DeviceId": "366d685f93f5477a8d29e8c45bae0a31",
              "Owner": "87cd2a6e407511e7922eb724f8803770",
              "Mtime": 1495681664335,
              "Ctime": 1495681664335,
              "Id": "d815ba2f84eb490b8e68d9dd744da397"
            }
          }
          ```

## Send Status
1. Transferring Gateway Status
    - URL: https://api.sandbox.thingplus.net/v2/gateways/{id}/status
        - {id}: Enter the ID of the gateway. Use the gateway ID registered above.
    - Method: PUT
    - Body:
        - Example

          ```Json
          {
            "ValidDuration": 450,
            "Value": "on"
          }
          ```
        - validDuration: means the duration (in seconds) for which `status` is valid. Typically you use 1.5 times the `reportInterval`.
        - value: The status of the gateway. You must send one of 'on', 'off', or 'err'.

    - Response
        - Example

          ```Json
          {
            "StatusCode": 200,
            "Message": "OK",
            "Data": {
              "Type": "status",
              "Value": "on",
              "SrcDbType": "gateway",
              "Time": "1495703469608",
              "ExpireAt": "1495703919608",
              "Vtime": "1495703469608",
              "Status": "87cd2a6e407511e7922eb724f8803770",
              "Owner": "87cd2a6e407511e7922eb724f8803770",
              "Gateway": "87cd2a6e407511e7922eb724f8803770",
              "Mtime": "1495703469610",
              "Ctime": "1495683245619",
              "Id": "status.gateway.pCMjRP"
            }
          }
          ```
        - expireAt: Indicates how long the `status` is valid, in Unix time in msec.
    - The gateway status must be sent once per `reportInterval`.
    - Even if the status of the gateway is `on`, after the expireAt time, you can not know what the gateway is.

2. Send Sensor Status
    - URL: https://api.sandbox.thingplus.net/v2/gateways/{owner}/sensors/{id}/status
        - {owner}: Enter the ID of the gateway to which the sensor is connected. Use the gateway ID registered above.
        - {id}: Enter the sensor ID. Use the sensor ID registered above.
    - Method: PUT
    - Body:
        - Example

          ```Json
          {
            "ValidDuration": 450,
            "Value": "on"
          }
          ```
        - validDuration: means the duration (in seconds) for which `status` is valid. Typically you use 1.5 times the `reportInterval`.
        - value: Status of the sensor. You must send one of 'on', 'off', or 'err'.

    - Response
        - Example

          ```Json
          {
            "StatusCode": 200,
            "Message": "OK",
            "Data": {
              "Type": "status",
              "Value": "on",
              "SrcType": "temperature",
              "SrcCategory": "sensor",
              "SrcDbType": "sensor",
              "Time": "1495715734508",
              "ExpireAt": "1495716184508",
              "Vtime": "1495715720489",
              "Status": "d815ba2f84eb490b8e68d9dd744da397",
              "Owner": "87cd2a6e407511e7922eb724f8803770",
              "Sensor": "d815ba2f84eb490b8e68d9dd744da397",
              "Mtime": "1495715734508",
              "Ctime": "1495715720489",
              "Id": "status.sensor.0uRmI2"
            }
          }
          ```
        - expireAt: Indicates how long the `status` is valid, in Unix time in msec.
    - The sensor status must be transmitted once per `reportInterval`.
    - Even if the status of the sensor is `on`, after the expireAt time, it is not possible to know what the sensor is.

## Send sensor value
1. Sending Sensor Value
    - URL: https://api.sandbox.thingplus.net/v2/gateways/{owner}/sensors/{id}/series
        - {owner}: Enter the ID of the gateway to which the sensor is connected. Use the gateway ID registered above.
        - {id}: Enter the sensor ID. Use the sensor ID registered above.
    - Method: PUT
    - Body:
        - Example
            - When transmitting one sensor value

              ```Json
              {
                "Value": "36.5",
                "Time": 1495715734508
              }
              ```
            - When sending multiple sensor values

              ```Json
              [
                {
                  "Value": "36.5",
                  "Time": 1495716734508
                },
                {
                  "Value": "36.3",
                  "Time": 1495717184508
                }
              ]
              ```

        - value: The sensor value. You must enter a string or object value and it must match the sensor type. However, if the sensor value is numeric, it is sent as a string.
        - time: The time at which the sensor value was measured, in Unix time in msec.
        - If you want to send multiple sensor values, you can send them in an array.

    - Response
        - Example
            - When one sensor value is transmitted

              ```Json
              {
                "StatusCode": 200,
                "Message": "OK",
                "Data": {
                  "Name": "Temperature sensor",
                  "Type": "temperature",
                  "DriverName": "openApiSensor",
                  "Model": "openApiTemp",
                  "Category": "sensor",
                  "DeviceId": "366d685f93f5477a8d29e8c45bae0a31",
                  "Owner": "87cd2a6e407511e7922eb724f8803770",
                  "Mtime": "1495717726517",
                  "Ctime": "1495681664335",
                  "Status": "status.sensor.0uRmI2",
                  "Series": "series.sensor.tOZhgI",
                  "Id": "d815ba2f84eb490b8e68d9dd744da397"
                }
              }
              ```
            - When multiple sensor values are transmitted

              ```Json
              {
                "StatusCode": 200,
                "Message": "OK",
                "Data": {
                  "Type": "series",
                  "SrcType": "temperature",
                  "SeriesPack": [
                    {
                      "Value": "36.5",
                      "Time": 1495718222169
                    },
                    {
                      "Value": "36.3",
                      "Time": 1495718672169
                    }
                  ],
                  "Mtime": "1495718691465",
                  "Ctime": "1495717726516",
                  "Time": "1495718672169",
                  "Value": "36.3",
                  "Owner": "87cd2a6e407511e7922eb724f8803770",
                  "Series": "d815ba2f84eb490b8e68d9dd744da397",
                  "Sensor": "d815ba2f84eb490b8e68d9dd744da397",
                  "SrcCategory": "sensor",
                  "SrcDbType": "sensor",
                  "Id": "series.sensor.tOZhgI"
                }
              }
              ```





