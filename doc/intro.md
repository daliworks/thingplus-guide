## Introduction
It explains the APIs provided by Thing+.

It is highly recommended that you read [Thing+ Developer Guide](https://github.com/daliworks/thingplus-guide) before you use Thing+ API. 

We provide Thing+ APIs for 3rd parties who want to build upon Thing+. The API is still being expanded.


## Possible scope
The resources accessible with Thing+ API are decided by the scope. 

You can refer to the detailed Scope [here](./OAuth2.md#Scopes)

## Requirement 
You need the authority for each resources to use Thing+ API and the authority can be obtained with `OAuth2`.

The detailed guide to `OAuth2` is refered [here](https://github.com/daliworks/thingplus-guide/blob/master/doc/OAuth2Guide_en.md).

The authorities for each resources can be available with `token`.

You need the preparation in advance to obtain `Token`

## preparation in advance and obtaining the Token

You need to create `authClient` in advance.

You create `authClient` with #endpoint:rQi8KjEqgw4J2HBy6 and obtaind `token` with `authClient`.

We offers two types to obtain OAuth token.

1. #endpoint:Pv7MmRuhWcoXziFPa
2. #endpoint:7RcNk9pBovabaZL96

You use the obtained token by putting it into the request's Header.

If you want to delegate resource privileges to specific users, take `1. Authorization Code grant` method.

If you want to access resources of management scope with the authority of administrator (Admin) other than specific user, please take `2. Resource owner password Credentials grant.`

You can find more datails [here](
https://github.com/daliworks/thingplus-guide/blob/master/doc/README_en.md#22-for-utilizing-oauthapp)

At API Document Site, we use `2. Resource owner password Credentials grant` for convenience.



## Notice
At <https://thingplus.api-docs.io>, you can not do #endpoint: rQi8KjEqgw4J2HBy6, which is a preparation process.

Create an `authClient` using a separate application.

At [following](http://support.thingplus.net/en/rest-api/getting-started.html#id-step1), to create `AuthClient` is explained in detail.

If you have successfully created `authClient`, you can now make a real request using` request try` in <https://thingplus.api-docs.io>.

Go to #endpoint: 7RcNk9pBovabaZL96 and use the `authClient` you created to get the` OAuth Token`

## How to use


Use the obtained `Token` in` Request Header`.

Use `token_type` and` access_token` of Token API `response`.

Add `Authorization` field to` Header` and input value in the form of `{token_type} {access_token}`.

ex) Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.ezcxfQ.BfgfVvKhvTOwlYHSzcFPQl-0c

Let's check the information of the user who acquired the privilege through the #endpoint: kwgNXKGY94NMQvfcX API.

If you have successfully received `Response`, everything is ready.

Explore and test other APIs.
