# Getting Started with the Thing+ REST APIs

## Step 1. Set up the system   
  - [Register a Thing+ service](https://iot.thingplus.net/#/register)
      - Or, your service may have already have been set up by our team
  - Hardware installation/procurement. See [list of Available Open Hardware](/en/open-hardware/openhardware-list.html)
  - If you are making an app, make sure your application can receveice web requests from Thing+
  - NOTE: Please check your Thing+ service's location before continuing
      - api.thingplus.net - This is the Japanese API server - if you registered your own service, this will be the API server you should use
      - api.thingplus.eu - This is the EU API server
      - api.sandbox.thingplus.net - This is a commercial API test server from Seoul
      ** You MUST ensure that you use the correct API server, depending on where your service (SERVICE_NAME.thingplus) is registered

## Step 2. Prepare Postman

### Step 2-1. Postman for getting started with the Thing+ REST API
  - Install [Google Chrome](http://www.google.com/chrome)
  - Install <a href="https://www.getpostman.com/docs/introduction" target="_blank">Postman</a>. <a href="https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop" target="_blank">Direct link for Chrome browser users</a>
  - You don't need to sign up, just click the 'Go to the app' button
      ![import](images/postman-first-launch.png)
  - Postman guide: <a href="https://www.getpostman.com/docs/launch" target="_blank">Launching Postman</a> and <a href="https://www.getpostman.com/docs/requests" target="_blank"> sending requests</a>

### Step 2-2. Import a Postman collection
  1. Click the 'Import' button

  ![import](images/import.png)

  2. Select 'Download from link'

  ![import link](images/import-link.png)

  3. Download [this](https://www.getpostman.com/collections/f1c2d8efb311d579eff6)

  4. Click 'Import' button and choose the downloaded file
  5. Close the module

### Step 2-3. Check the imported collection

  - Select the 'Collections' tab and then select the 'Getting Started with the Thing+ REST API' collection

  ![collection](images/collection.png)

## Step 3. Register Client ID & Client Secret Key with Thing+

> This step prepares your application for OAuth. This step does not involve user credentials, all credentials mentioned are for your application. Normally you should only do this **ONCE** per application, unless your application require complex ACL and roles management

1. Open Chrome browser then <a href="https://www.thingplus.net/#/login" target="_blank">Sign in </a> to the Thing+ Portal

![interceptor enable](images/sign-in.png)

2. Launch Postman

3. Enable interceptor

![interceptor enable](images/interceptor-enable.png)

4. [Install interceptor](https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo)

![interceptor enable](images/interceptor-install.png)

5. Getting a Client ID and Secret

![interceptor enable](images/oauth-client-id-secret.png)

- Select **_Getting a client ID and secret_** on the collection
- Select the _Body_ tab
- Select _raw_
- Put your OAuth client ID in the `reqId` field. This should be unique across all applications connected to Thing+. You may choose any ID here - something simple and easy to remember is fine.
- Put your OAuth client secret in the `clientSecret` field. You may choose anything as your OAuth Client Secret - consider it a password of sorts. These two fields (client ID and Client Secret) should not be exposed to anyone. Keep it **secret**
- Put the name of your application into the `name` field. This is used to identify your application. You should put the name of your company or service here, along with something to make it unique. (If Thing+ has any other application with the same name, you will run into an error). For example, leland_0144 is a much better application name then "leland".
- Change the field `scopes` to determine the rights for your application. Read more about acceptable scopes [here](./OAuth2.md)
- Click the _Send_ button

6. Result should display **201 Created**

![interceptor enable](images/oauth-client-id-secret-success.png)

7. Disable interceptor

![interceptor disable](images/interceptor-disable.png)

## Step 4. Get OAuth Access token with [Authorization Code Grant](./OAuth2.md#oauth-20-grant-types)

> This step authorizes the user with Thing+ via your application

> An Access token Expires in 15 days. This may be changed later without prior notification. Please check back often

1. Prepare login page for your application
2. When the user logins, redirect them to this URL

```
https://api.thingplus.net/v2/oauth2/authorize?response_type=code&client_id={CLIENT_ID}&redirect_uri={REDIRECT_URI}
``` 

  - Replace `{CLIENT_ID}` with the Thing+ OAuth Client ID you used as your reqID in steps 3-1 to 3-6
  - Replace `{REDIRECT_URI}` with your callback URL. This URL should we able to take a 'code' parameter. For example `http://yoururl/?code={AUTHORIZATION_CODE}`

  ![OAuth authorization screen](images/oauth-authorize.png)

3. User should click the 'Allow' button

4. Thing+ will redirect back to your `{REDIRECT_URI}` with the "code" in your query string
  ![interceptor enable](images/oauth-code.png)

5. Exchange code for an OAuth Access token

> This step should be automated in your code, the method below is for demonstration purpose only

![exchange code with postman](images/oauth-exchange-code.png)
- Select **Exchange code for an OAuth Access token** from the collection
- Select _Body_ tab
- Select _x-www-form-urlencoded_ 
- Add `{AUTHORIZATION_CODE}` you received from the last step to `code` field
- Fill in the client ID for your appliction in `client_id`
- Fill in the client secret for your application in `client_secret`
- Fill in the redirect URL. This URL should be the same with the redirect URL from step 2
- Click the 'Send' button

5. Result should say "200 OK" and provide you with an access_token

  ![interceptor enable](images/oauth-access-token.png)

## Step 5. Using Thing+ REST API with an OAuth Access token

### Step 5-1. Create a [Postman Environment](https://www.getpostman.com/docs/environments)

> This step is for trying out API with POSTMAN, you can skip this part if you are preparing for your application

1. Launch Postman

2. Select 'Manage environments'

![environment](images/environment.png)

3. Click the 'Add' button

![environment add](images/environment-add.png)

4. Add a 'Key' and 'Value' and Click the 'Submit' button

![environment submit](images/environment-submit.png)

- Add 'Thing+ production' to 'New environment' field.
- Add **AccessToken** (Case Sensitive) to `Key` field.
- Add your OAuth Access Token to `Value` field.
- Close the dialog

5. Select 'Thing+ production'

![import](images/environment-select.png)

6. Try sending a request. **Now you are ready to use the Thing+ REST API with an OAuth Access token**. Your requests should look similar to this

![environment variable](images/environment-variable.png)


### Step 5-2. Authorization in your app

When you are sending requests to the Thing+ API, be sure to include the token you acquired from step 4 into the header with

```
Authorization: Bearer {AccessToken}
```

<div id='id-step3'></div>

## Step 6. Tips and Tricks for working with the Thing+ API

### Postman lets you generate code snippets in more than 15 languages.
From [Writing front-end API code with Postman](http://blog.getpostman.com/2015/08/31/writing-front-end-api-code-with-postman)

![Code generation](images/postman-code.png)

### Reading gateway information
  - Select **_Reading gateways_** in the collection and Click the 'Send' button
  - You can get your gateways's ID
  - Request URL: [GET] `https://api.thingplus.net/v2/gateways`
  - Response type is Object.

  ![http header](images/reading-gateways.png)

### Reading gateway information including filters
  - Select a **_Reading gateways_** on the collection and Click the 'Send' button.
  - Request URL: [GET] `https://api.thingplus.net/v2/gateways?count=10`
  - <a href="https://thingplus.api-docs.io/2.0/getting-started/query-string" target="_blank">Accepted Parameters</a>
  - Response type is Object
