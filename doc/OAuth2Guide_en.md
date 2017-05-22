# Thing+ OAuth2 Guide
This is a simple guide to using Thing+ with 3rd party resources.
It will help you acquire authentication & authorization using OAuth2.
See here for details [Link](./OAuth2.md)

## What is OAuth2?
https://oauth.net/2/

![OAuth](./images/oauth2.png "OAuth")


## Initial Setup
1. Tools for API testing
    - Postman: https://www.getpostman.com/
    - Fiddler: http://www.telerik.com/fiddler
    - DHC: https://client.restlet.com/
2. authClient creation
    - Refer to the authClients entry in api guide to create authClient
    - Separate maintenance / management required for generated authClient
 
## [Scopes](./OAuth2.md#scopes)
Scopes let you specify exactly what type of access you need. Scopes limit access for OAuth tokens. They do not grant any additional permission beyond that which the user already has.

[More](./OAuth2.md#scopes)


## [Authorization Code system](./OAuth2.md#authorization-code-grant-or-web-server)
Receiving delegation for the specified privilege of a specific user

1. Move to the thing+ login page - required for oauth2 / authorization API usage
2. Login if not already logged in. If you are already logged in, go to the next step
3. Obtain code from query of the redirected URL
4. Obtain access_token via oauth2 / token API
    * The token is valid for 15 days and maintenance / management is required.
5. Use the acquired token in the API
    * Add Authorization field to the Request Header
    * The value is filled with Token_Type and access_token utilization value of the token API response
    * {token_type} {access_token} Type
    * ```Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiIyIiwiY2xpZW50SWQiOiJzd2l0aGVyIiwiaWF0IjoxNDkxMjc1MTMxLCJleHAiOjE0OTI1NzExMzF9.bG1pusWH5pwJ4_BxQ-v0tmgkqMix3H82uUSxZycBWOo```
6. Develop using the above procedure



## [Resource Owner Password Credentials Method](./OAuth2.md#resource-owner-password-credentials-grant)
Access the resources in your service using the privileges of a serviceAdmin.

1. Obtain access_token via oauth2 / token API
    * The token is valid for 90 days and maintenance / management is required
2. Use the acquired token in the Thing+ API
    * Add Authorization field to Request Header
    * The value is filled with Token_Type and access_token utilization value of the token API response
    * {Token_type} {access_token} Type
    * ```Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiIyIiwiY2xpZW50SWQiOiJzd2l0aGVyIiwiaWF0IjoxNDkxMjc1MTMxLCJleHAiOjE0OTI1NzExMzF9.bG1pusWH5pwJ4_BxQ-v0tmgkqMix3H82uUSxZycBWOo```
3. Develop using the above procedure
4. When data is accessed by the serviceAdmin, multiple users' data can be accessed

## In Detail
[Link](./OAuth2.md)
