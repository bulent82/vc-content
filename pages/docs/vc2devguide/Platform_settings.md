---
title: Platform settings
layout: docs
date: 2016-06-08T12:59:50.447Z
permalink: /docs/vc2devguide/Platform+settings
---

  


**VirtoCommerce.Platform.Web\Web.config** file contains global application settings and connection strings.

# Connection strings

## VirtoCommerce

This is a standard database connection string. It defines SQL server, database, user and password.

## AssetsConnectionString

Assets connection string consists of two parts. First part is **provider=XXXX**, which specifies which provider to use for storing assets. The remainder of the string is passed to provider’s constructor. Platform includes two asset providers: LocalStorage and AzureBlobStorage.

### LocalStorage

<add name="AssetsConnectionString" connectionString="provider=LocalStorage;rootPath=~/App_Data/Assets;publicUrl=http://localhost/admin/Assets" />

This provider stores assets in a local file system.

**rootPath** is a virtual or physical path to the assets root directory.

**publicUrl** is a public URL for the root directory defined above. It is used to construct full asset URLs.

### AzureBlobStorage

<add name="AssetsConnectionString" connectionString="provider=AzureBlobStorage;DefaultEndpointsProtocol=http;AccountName=XXXX;AccountKey=YYYY" />

This provider stores assets in Azure Storage.

You should copy values for this connection string from your Azure portal and paste it to web.config

# Application settings

## SampleDataUrl

<add key="VirtoCommerce:SampleDataUrl" value="http://virtocommerce.blob.core.windows.net/sample-data" />

This parameter defines the URL of either a ZIP package, which contains exported sample data, or a directory containing the manifest.json file with the list of available sample data packages and its URLs.

## ModulesDataSources

<add key="VirtoCommerce:ModulesDataSources" value="https://raw.githubusercontent.com/VirtoCommerce/vc-modules/master/modules.json; C:\customModules\modules.json" />

This parameter defines the available data sources for VC modules management. There can be multiple (remote or local) links specified in a single setting value. Each link should lead to file in **json** format containing modules information such as module id, title, version, dependencies, authors, etc.

## Authentication settings

The platform includes a number of authentication providers, each of which can be enabled or disabled separately.

### Cookies

<add key="VirtoCommerce:Authentication:Cookies.Enabled" value="true" /><add key="VirtoCommerce:Authentication:Cookies.ValidateInterval" value="1:00:00:00" />If the time passed since the authentication cookie was generated is greater than ValidateInterval the security stamp validator will check if the security stamp has been changed in the database.

Default value is 1 day.

### Bearer Tokens

<add key="VirtoCommerce:Authentication:BearerTokens.Enabled" value="true" /><add key="VirtoCommerce:Authentication:BearerTokens.AccessTokenExpireTimeSpan" value="1:00:00" />AccessTokenExpireTimeSpan is the life time of the access token. When this period has expired the client should request a new token.

Default value is 1 hour.

### HMAC

<add key="VirtoCommerce:Authentication:Hmac.Enabled" value="true" /><add key="VirtoCommerce:Authentication:Hmac.SignatureValidityPeriod" value="00:20:00" />If the time passed since the request signature was generated is greater than SignatureValidityPeriod the request will be rejected by server.

Default value is 20 minutes.

### API Keys

<add key="VirtoCommerce:Authentication:ApiKeys.Enabled" value="true" /><add key="VirtoCommerce:Authentication:ApiKeys.HttpHeaderName" value="api_key" /><add key="VirtoCommerce:Authentication:ApiKeys.QueryStringParameterName" value="api_key" />The API key can be passed in the Authorization header, in the custom header (HttpHeaderName) or in the URL (QueryStringParameterName).

Default value for both parameters is api_key.


