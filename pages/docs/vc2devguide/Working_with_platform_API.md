---
title: Working with platform API
layout: docs
date: 2016-05-31T14:56:15.227Z
permalink: /docs/vc2devguide/Working+with+platform+API
---

## Platform API authentication configuration 

VirtoCommerce platform support two authentication types for API calls

* Simple - when user id passed in url for  each API request  example: [http://demo.virtocommerce.com/admin/api/catalog/catalogs?api_key=a348fa7508d342f6a32f8bf6c6681a2a%20](http://demo.virtocommerce.com/admin/api/catalog/catalogs?api_key=a348fa7508d342f6a32f8bf6c6681a2a%20)
* HMAC - Hash-based message authentication code (HMAC) is used to to identify a client and ensure the request integrity  


To allow use platform API you previous should create  user account in manager and generate API key with appropriator type (simple or HMAC) 

### Create user

You need to create new user through manager. Login to VirtoCommerce admin with administrator permissions. Navigate to Configuration -> Security -> Users. 

Next to unable use platform API need assign to user special role** Use api **with one  permission **security:call_api**. More on permissions read: [Working with platform security](http://docs.virtocommerce.com/display/vc2devguide/Working+with+platform+security). 

![](../../assets/images/docs/image2016-5-31_16-54-3.png)

After the permissions has been set click "Create". The new user will be created and user edit blade will open.

### Generate HMAC API key 

Open **Configuration > Security > Users**.Select a userClick **API Keys** widgetClick **Add** button in the toolbarSelect **Hmac** as Key typeClick **Ok** button in the API key bladeClick **Save** button in the User information blade  


![](../../assets/images/docs/image2016-5-30_11-0-24.png)

### Generate Simple API key 

Repeat 1-5 above stepsSelect **Simple **as Key typeClick **Ok** button in the API key bladeClick **Save** button in the User information blade## Using platform API from managed code

 To use API in your managed code need generate client library first. 

[[How to generate module API C#client|How to generate module API C]]

Next you should install special [VirtoCommerce.Platform.Client.Security](https://www.nuget.org/packages/VirtoCommerce.Platform.Data.Security)  NuGet package which allows to use both (HMAC and SImple) API authentication protocols.

### Using API with HMAC authentication

```
// HMAC credentialsÂ 
// that is the App ID generated while creating HMACkey for the user.
var apiAppId = "your API id";
// that is the Secret key generated while creating HMAC key for the user.
 var apiSecretKey = "your API secret key";
// Create HMAC headers handler which will add to each request special auth headers
 var hmacHandler = new HmacRestRequestHandler(apiAppId, apiSecretKey);
// Create rest client 
 var apiClient = new ApiClient("platform API url", new VirtoCommerce.Client.Client.Configuration(), hmacHandler.PrepareRequest);
Â 
// Create configuration variable to be used by all api modules
var config = new VirtoCommerce.Client.Client.Configuration(apiClient)
//create catalog client to call catalog api methods
var catalogClient = new CatalogModuleApi(config);
 
//get all catalogs
var catalogs = catalogClient.CatalogModuleCatalogsGetCatalogs();
```

### Using API with Simple authentication

```
// Simple auth key
// that is the authentication key generated for user
var apiKey= "your API key";
// Create simple headers handler which will add to each request query string ?api_key parameter
var simpleHandler = new SimpleKeyRestRequestHandler(apiKey);
// Create rest client 
 var apiClient = new ApiClient("platform API url", new VirtoCommerce.Client.Client.Configuration(), simpleHandler.PrepareRequest);
 
// Create configuration variable to be used by all api modules
var config = new VirtoCommerce.Client.Client.Configuration(apiClient)
//create catalog client to call catalog api methods
var catalogClient = new CatalogModuleApi(config);
 
//get all catalogs
var catalogs = catalogClient.CatalogModuleCatalogsGetCatalogs();
```

 

## Using platform API from JavaScript 

###   
Using API with Simple authentication

 Nothing to special just add ?api_key='Your API key' to each API request 

Example:

http://demo.virtocommerce.com/admin/api/catalog/catalogs?api_key=a348fa7508d342f6a32f8bf6c6681a2a%20###   
Using API with HMAC authentication

#### Constructing the request

When using HMAC authentication each request to the API should include the following HTTP header:

|Name|Value|
|----|-----|
|Authorization|HMACSHA256 AppId;Timestamp;Signature|

Example:

Authorization: HMACSHA256 27e0d789f12641049bd0e939185b4fd2**;**2016-02-09T13:24:20.837Z**;**e82bbded532a80bf744f70a86506ddbe94e0e8653304ad67819d8e280e52282f

|HMACSHA256|Authorization type|
|AppId|The client ID|
|Timestamp|Date and time when the request has been constructed (in ISO 8601 format)|
|Signature|The HEX string representing the hash of the AppId and Timestamp calculated with HMACSHA256 algorithm|

#### Calculating the signature

Though the following code examples are written in JavaScript, the steps are the same for any language.

Include the HMAC implementation from Google Code:

<script src="http://crypto-js.googlecode.com/svn/tags/3.1.2/build/rollups/hmac-sha256.js"></script>1. Build the timestamp string by converting current date and time to string in the ISO 8601 format:

var timestampString = new Date().toISOString();
2. Build the message string by concatenating the AppId and timestamp string and separating them with the ampersand character:

var message = appId + '&' + timestampString;
3. Calculate the message hash by using the HMACSHA256 algorithm with your secretKey:

var hash = CryptoJS.HmacSHA256(message, CryptoJS.enc.Hex.parse(secretKey));4. Build the authorization header value by concatenating the AppId, timestamp and hash and separating them with the semicolon character:

var headerValue = 'HMACSHA256 ' + appId + ';' + timestampString + ';' + hash;
5. Add authorization header to the request:

$.ajax({ url: '[http://localhost/admin/api/platform/security/currentuser](http://localhost/admin/api/platform/security/currentuser)', headers: { Authorization: headerValue } })#### JavaScript test client

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Using HMAC authentication for Virto Commerce in JavaScript</title>
    <style>
        .label {
            margin-top: 1em;
            font-weight: bold;
        }
 
        .text-input {
            width: 30em;
        }
    </style>
    <script src="https://code.jquery.com/jquery-2.2.0.min.js"></script>
    <script src="http://crypto-js.googlecode.com/svn/tags/3.1.2/build/rollups/hmac-sha256.js"></script>
    <script type="text/javascript">
        $(function () {
            $('#button').click(sendRequest);
 
            var progress = $("#progress");
            progress.hide();
 
            function sendRequest() {
                var appId = $("#app-id");
                var secretKey = $("#secret-key");
                var api = $("#api");
                var header = $("#header");
                var response = $("#response");
 
                var headerValue = generateAuthorizationHeaderValue(appId.val(), secretKey.val());
 
                header.text(headerValue);
                progress.show();
 
                $.ajax({
                    url: api.val(),
                    headers: { Authorization: headerValue }
                }).done(function (data) {
                    response.text(JSON.stringify(data));
                }).fail(function (jqXhr, textStatus, errorThrown) {
                    response.text('ERROR: ' + errorThrown);
                }).always(function () {
                    progress.hide();
                });
            }
 
            function generateAuthorizationHeaderValue(appId, secretKey) {
                var timestampString = new Date().toISOString();
                var message = appId + '&' + timestampString;
                var hash = CryptoJS.HmacSHA256(message, CryptoJS.enc.Hex.parse(secretKey));
                var headerValue = 'HMACSHA256 ' + appId + ';' + timestampString + ';' + hash;
                return headerValue;
            }
        });
    </script>
</head>
<body>
    <div class="label">App ID</div>
    <input id="app-id" class="text-input" type="text" value="27e0d789f12641049bd0e939185b4fd2" />
    <div class="label">Secret Key</div>
    <input id="secret-key" class="text-input" type="text" value="34f0a3c12c9dbb59b63b5fece955b7b2b9a3b20f84370cba1524dd5c53503a2e2cb733536ecf7ea1e77319a47084a3a2c9d94d36069a432ecc73b72aeba6ea78" />
    <div class="label">URL</div>
    <input id="api" class="text-input" type="text" value="http://localhost/admin/api/platform/security/currentuser" />
    <input id="button" type="button" value="Send Request" />
    <span id="progress">Sending request...</span>
    <div class="label">Authorization header value</div>
    <div id="header"></div>
    <div class="label">Response</div>
    <div id="response"></div>
</body>
</html>
```


