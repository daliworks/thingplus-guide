# Getting Started with the Thing+ REST APIs

## Step 1. Thing+ Service registration & Hardware installation

### Step 1-1
  - Thing+ service registration is required before you start
    - <a href="http://support.thingplus.net/en/user-guide/registration.html" target="_blank">Thing+ service registration</a>

### Step 1-2
  - Hardware installation/procurement is next
    - [List of Available Open Hardware](/en/open-hardware/openhardware-list.html)

## Step 2. Prerequisites

### Step 2-1. Postman for getting started with the Thing+ REST API
  - Install <a href="http://www.google.com/chrome" target="_blank">Google Chrome</a>
  - Install <a href="https://www.getpostman.com/docs/introduction" target="_blank">Postman</a>
    - <a href="https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop" target="_blank">Direct link for Chrome browser users</a>
    - You don't need to sign up, just click the 'Go to the app' button
      <br> ![import](images/postman-first-launch.png)
    - Postman guide
      - <a href="https://www.getpostman.com/docs/launch" target="_blank">Launching Postman</a> and <a href="https://www.getpostman.com/docs/requests" target="_blank"> sending requests</a>

### Step 2-2. Import a Postman collection
  1. Click the 'Import' button
<br> ![import](images/import.png)
<br><br>
  2. Select 'Download from link'
<br>![import link](images/import-link.png)
    - Add the below link
      - https://www.getpostman.com/collections/f1c2d8efb311d579eff6
    - Click the 'Import' button
<br><br>
  3. Close the module

### Step 2-3. Check the imported collection

  1. Select the 'Collections' tab and then select the 'Getting Started with the Thing+ REST API' collection

<br> 
![collection](images/collection.png)


### Step 2-4. Creating a Thing+ OAuth Client ID & Client Secret Key

1. Open Chrome browser then <a href="https://www.thingplus.net/#/login" target="_blank">Sign in </a> to the Thing+ Portal
<br> ![interceptor enable](images/sign-in.png)
<br><br>
2. Launch Postman
<br><br>
3. Enable interceptor
<br> ![interceptor enable](images/interceptor-enable.png)
<br><br>
4. Install interceptor
<br> https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo
<br> ![interceptor enable](images/interceptor-install.png)
<br><br>
5. Getting a Client ID and Secret
<br> - HTTP Method: POST
<br> ![interceptor enable](images/oauth-client-id-secret.png)
<br> 1) Select a **_Getting a client ID and secret_** on the collection
<br> 2) Select a 'Body' tab
<br> 3) Select a 'raw'
<br> 4) Add a "reqId" for OAuth2.0 client credentials
<br>&nbsp;&nbsget-oauth-access-token-api-keyp;&nbsp;&nbsp;• Client ID is used to identify the application using Thing+ Rest API
<br>  5) Add a "clientSecret" for OAuth2.0 client credentials
<br>&nbsp;&nbsp;&nbsp;&nbsp;• Client Secret is used to authenticate the identity of the application using Thing+ Rest API
<br>  6) Add a "name"
<br>&nbsp;&nbsp;&nbsp;&nbsp;• This name is used to request access a user's account
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ex) your company or service name
<br> 7) You can change <a href="./oauth2.html#scopes" target="_blank">"Scopes"</a> if you need any change
       Scopes limit access for OAuth tokens
<br> 8) Click the 'Send' button
<br><br>
6. Check the '201 Created' result status
<br> ![interceptor enable](images/oauth-client-id-secret-success.png)
<br><br>
7. Disable interceptor
<br> ![interceptor disable](images/interceptor-disable.png)


### Step 2-5. Obtaining an OAuth Access token with <a href="./OAuth2.md#oauth-20-grant-types" target="_blank">Authorization Code Grant</a> type

___An Access token Expires in 15 days (possibly can be changed without advance notification)___

1. Launch Chrome browser with below URL
  - replace **{CLIENT_ID}** and **{REDIRECT_URI}** to your Client ID and your Service URI
  - https://api.thingplus.net/v2/oauth2/authorize?response_type=code&client_id={CLIENT_ID}&redirect_uri={REDIRECT_URI}
    - **{CLIENT_ID}** : Thing+ OAuth Client ID to received at Step 1-4
    - **{REDIRECT_URI}** : The URL in your app where users will be sent after authorization
      - Ex) http://www.daliworks.net
  ![interceptor enable](images/oauth-authorize.png)
<br><br>
2. Click the 'Allow' button
<br><br>
3. Then Thing+ redirects back to your {redirect_uri} with "code" in url
  ![interceptor enable](images/oauth-code.png)
<br><br>
4. Exchange code for an OAuth Access token
<br> - HTTP Method: POST
<br> ![interceptor enable](images/oauth-exchange-code.png)
<br> 1) Select a **_Exchange code for an OAuth Access token_** on the collection
<br> 2) Select a 'Body' tab
<br> 3) Select a 'x-www-form-urlencoded' (application/x-www-form-urlencoded)
<br> 4) Add a "code" in url above
<br>&nbsp;&nbsp;&nbsp;&nbsp;• The code you received as a response in url above
<br> 5) Add a your "client_id"
<br>&nbsp;&nbsp;&nbsp;• The client ID you received from Thing+ when you registered your application
<br> 6) Add a your "client_secret"
<br>&nbsp;&nbsp;&nbsp;• The client secret you received from Thing+ when you registered your application
<br> 7) Add a your "redirect_uri"
<br>&nbsp;&nbsp;&nbsp;• The redirect URL when you registered your application
<br> 8) Click the 'Send' button
<br><br>
5. Check the '200 OK' result status and Access token

  ![interceptor enable](images/oauth-access-token.png)


## Step 3. Using the Thing+ REST API with an OAuth Access token

### Step 3-1. Create a <a href="https://www.getpostman.com/docs/environments" target="_blank">Postman Environments</a>

1. Launch Postman

2. Select the 'Manage environments'
![environment](images/environment.png)

3. Click the 'Add' button
![environment add](images/environment-add.png)

4. Add a 'Key' and 'Value' and Click the 'Submit' button
![environment submit](images/environment-submit.png)
- Add a 'Thing+ Access Token' to 'New environment' field.
- Add a **AccessToken** (Case Sensitive) to 'Key' field.
- Add a your OAuth Access Token to 'Value' field.
- Close the modal

5. Select a 'Thing+ Access Token'
![import](images/environment-select.png)

**Now you are ready to use the Thing+ REST API with an OAuth Access token**

- 'Getting Started with the Thing+ REST API' collection uses {{AccessToken}} variable for the 'Authorization' http header
![environment variable](images/environment-variable.png)

<div id='id-step3'></div>

## Step 4. Try some APIs

#### **_Useful tip before trying some APIs with postman_**
  - Postman lets you generate code snippets in more than 15 languages.
  - <a href="http://blog.getpostman.com/2015/08/31/writing-front-end-api-code-with-postman" target="_blank">Writing front-end API code with Postman</a>
  ![environment variable](images/postman-code.png)

### Gateway
  - Reading gateways
    - Select a **_Reading gateways_** on the collection and Click the 'Send' button.
      - You can get your gateways's ID
    - Request URL
      - [GET] https://api.thingplus.net/v2/gateways
      - The response type is Object.

    ![http header](images/reading-gateways.png)

  - Reading gateways with queries
    - Select a **_Reading gateways_** on the collection and Click the 'Send' button.
    - Request URL
      - [GET] https://api.thingplus.net/v2/gateways?count=10
      - <a href="https://thingplus.api-docs.io/2.0/getting-started/query-string" target="_blank">Table for Query Parameters</a>
      - The response type is Object