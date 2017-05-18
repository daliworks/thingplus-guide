
# OAuth2

OAuth2 is a protocol that lets external apps request authorization to private details in a user’s ThingPlus account without getting their password.

All developers need to register their application before getting started. A registered OAuth application is assigned a unique Client ID and Client Secret. The Client Secret should not be shared.

(NOTE: Registration of application is not ready now. Contact ThingPlus administrator until we are ready)

## OAuth 2.0 Grant Types    

### Authorization Code Grant (or Web Server)
#### Step 1
Redirect the user to allow or not for the Web Server(or Confidential Client) to access the resources of the user with registered scopes

```json
GET https://api.thingplus.net/v1/oauth2/authorize

Example>
  GET https://api.thingplus.net/v1/oauth2/authorize?client_id={CLIENT_ID}&response_type=code&redirect_uri={REDIRECT_URI}
```

* URL Query parameters

|      Name     |      Type     |                         Description                          
| ------------- | ------------- | ------------------------------------------------------------ 
| client_id     | string        | __Required__ The client ID you received from thingplus
| response_type | string        | __Required__ Use "code"
| redirect_uri  | string        | __Required__ The URL in your app where users will be sent after authorization.

#### Step 2
ThingPlus redirects back to your site with "code" in url when the user accepted your request

```json
{REDIRECT_URI}/?code={AUTHORIZATION_CODE}
```

#### Step 3
Exchange code for an Access token

```
POST https://api.thingplus.net/v1/oauth2/token

Content-Type : application/x-www-form-urlencoded
```

* Body parameters

|      Name     |      Type     |                         Description                          
| ------------- | ------------- | ------------------------------------------------------------ 
| code          | string        | __Required__ The code you received as a response from Step 2
| grant_type    | string        | __Required__ Use "authorization_code"
| redirect_uri  | string        | __Required__ The redirect URL when you registered your application
| client_id     | string        | __Required__ The client ID you received from thingplus when you registered your application
| client_secret | string        | __Required__ The client secret you received from thingplus when you registered your application


### Resource Owner Password Credentials Grant
#### Step 1
Get an Access token with resource owner(user) password credentials

NOTE: This grant is not allowed for the 3rd party applications

```
POST https://api.thingplus.net/v1/oauth2/token

Content-Type : application/x-www-form-urlencoded
```

* Body parameters

|      Name     |      Type     |                         Description                          
| ------------- | ------------- | ------------------------------------------------------------ 
| grant_type    | string        | __Required__ Use "password"
| client_id     | string        | __Required__ The client ID you received from thingplus when you registered your application
| client_secret | string        | __Required__ The client secret you received from thingplus when you registered your application
| username      | string        | __Required__ The username of the resource owner(user)
| password      | string        | __Required__ The password of the resource owner(user) - MD5 Hash code

> NOTE: password must be MD5 hash code. For more information visit [JavaScript-MD5](https://github.com/blueimp/JavaScript-MD5)


## Limitations
* Authorization code
  - Expire in 10 minutes
  - Exchange for the Access token is possible only one time

* Access token
  - Authorization Code Grant: Expire in 15 days
  - Resource Owner Password Credentials Grant: Expire in 90 days
  - Possibly can be changed without advance notification

## Scopes
Scopes let you specify exactly what type of access you need. Scopes limit access for OAuth tokens. They do not grant any additional permission beyond that which the user already has.

For the Authorization Code Grant, requested scopes will be displayed to the user on the authorize form.

|     Scope          |                Name              |                         Description
| ------------------ | -------------------------------- | ------------------------------------------------------------ 
| (no scope)         |                                  | Cannot access any scopes
| user-profile       | User Profile Read and Update     | ___TBD___ Read and update the profile of the user
| user-profile-read  | User Profile Read                | Read the profile of the user
| gateway            | Gateway Ceate/Read/Update/Delete | ___TBD___ Register a gateway/device/sensor and read, update, delete gateways/devices/sensors for which the user has permissions
| gateway-read       | Gateway Read                     | Read gateways/devices/sensors and control actuator for which the user has permissions
| gateway-update     | Gateway Read/Update              | Read and update gateways/devices/sensors, control actuator, and manage the gateways for which the user has permissions
| timeline-read      | Timeline Read                    | Read timelines of the user
| tag                | Tag Ceate/Read/Update/Delete     | Create, read, update and delete tags of the user
| tag-read           | Tag Read                         | Read tags of the user
| rule               | Rule Read/Update/Delete          | ___TBD___ Read, update and delete rules of the user
| rule-read          | Rule Read                        | Read rules of the user
| service-read       | Service Read                     | Read service for which the user is registered
| site-read          | Site Read                        | Read site in which the user is registered
| billing-read       | Billing Read                     | ___TBD___ Read billing information of the user

___TBD___ : Not available now

## Errors
### Errors for the authorization request
* Missing required parameter
  * If the client_id or response_type or redirect_uri is not provided, you will receive invalid_request AuthorizationError

```json
{
  "name": "AuthorizationError",
  "message": "Missing required parameter: response_type",
  "code": "invalid_request",
  "status": 400
}
```

* Unsupported Response type
  * If you request with unsupported response type, you will receive unsupported_response_type AuthorizationError

```json
{
  "name": "AuthorizationError",
  "message": "Unsupported response type: code2",
  "code": "unsupported_response_type",
  "status": 501
}
```

* Unauthorized Client ID
  * If the client_id is not existing or not allowed to use, you will receive unauthorized_client AuthorizationError

```json
{
  "name": "AuthorizationError",
  "message": "The client_id is incorrect",
  "code": "incorrect_client_credentials",
  "status": 401
}
```

* Mismatched Redirect URI
  * If the redirect_uri you registered for the application does not match the redirect_uri of the request, you will receive redirect_uri_mismatch AuthorizationError

```json
{
  "name": "AuthorizationError",
  "message": "Mismatched redirect_uri",
  "code": "redirect_uri_mismatch",
  "status": 400
}
```

* Denied from the User
  * If the user denied your request, you will be redirected back to your site with error in url

```json
{REDIRECT_URI}/?error=access_denied
```

* Forbidden request
  * If the user accepted at the authorization grant page and accept again in the same page, the user will receive ForbiddenError

```json
{
  "name": "ForbiddenError",
  "message": "Unable to load OAuth 2.0 transaction: xxffggxxaf",
  "status": 403
}
```

### Errors for the access token request
* Unsupported Grant type
  * If you request with unsupported grant type, you will receive unsupported_grant_type TokenError

```json
{
  "name": "TokenError",
  "message": "Unsupported grant type: password2",
  "code": "unsupported_grant_type",
  "status": 501
}
```

* Expired Authorization code
  * If the authorization code is expired, you will receive expired_code TokenError

```json
{
  "name": "TokenError",
  "message": "Authorization code is expired",
  "code": "expired_code",
  "status": 403
}
```

* Invalid Authorization code
  * If the authorization code is not correct or not valid, you will receive invalid_code TokenError

```json
{
  "name": "TokenError",
  "message": "Authorization Code is invalid",
  "code": "invalid_code",
  "status": 400
}
```

* Mismatched Redirect URI
  * If the redirect_uri you registered for the application does not match the redirect_uri of the request, you will receive redirect_uri_mismatch TokenError

```json
{
  "name": "TokenError",
  "message": "Mismatched redirect_uri",
  "code": "redirect_uri_mismatch",
  "status": 400
}
```

* Incorrect Client credentials
  * If client_id and/or client_secret are not correct, you will receive incorrect_client_credentials TokenError

```json
{
  "name": "TokenError",
  "message": "The client_id and/or client_secret are incorrect",
  "code": "incorrect_client_credentials",
  "status": 401
}
```

* Incorrect User credentials
  * If username and/or password are not correct, you will receive incorrect_user_credentials TokenError

```json
{
  "name": "TokenError",
  "message": "The username and/or password are incorrect",
  "code": "incorrect_user_credentials",
  "uri": null,
  "status": 401
}
```

* Unauthorized User
  * If the user is unauthorized, you will receive unauthorized_user TokenError

```json
{
  "name": "TokenError",
  "message": "The user is unauthorized",
  "code": "unauthorized_user",
  "uri": null,
  "status": 403
}
```

### Errors for API request with the access token
* Invalid Access token
  * If the Access token is not valid or not correct, you will receive JsonWebTokenError

```json
{
  "name": "JsonWebTokenError",
  "message": "invalid token"
}
```

* Invalid Signature
  * If the secret key to generate the Access token is changed, you will receive JsonWebTokenError

  > NOTE: If you receive this error, you must get new Access token from the user

```json
{
  "name": "JsonWebTokenError",
  "message": "invalid signature"
}
```

* Expired Access token
  * If the Access token is expired, you will receive TokenExpiredError

```json
{
"name": "TokenExpiredError",
"message": "jwt expired",
"expiredAt": "2015-06-10T10:10:34.000Z"
}
```

-----

```
Copyright (c) 2015, Daliworks. All rights reserved.
Reproduction and/or distribution in source and binary forms
without the written consent of Daliworks, Inc. is prohibited.
```
