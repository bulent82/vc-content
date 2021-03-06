---
title: How to generate module API C# client
layout: docs
date: 2016-07-27T10:29:39.577Z
permalink: /docs/vc2devguide/How+to+generate+module+API+C%23+client
---

This document describes how to setup the environment, build and update an API client for VirtoCommerce platform module.

## Table of contents

  


## Preparing building environment and swagger-codegen

**The next steps are required only if you're **building the API client for **the first time.**

Download apache maven from [http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi) (download the binary zip archive "Binary zip archive")

Unzip the archive

Install Java JDK from [http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

Set system environment variables to maven ~\bin folder (Path: c:\apache-maven-3.3.9\bin\) & jdk (JAVA_HOME: C:\Program Files\Java\jdk1.8.0_92)

Clone *swagger-codegen* repository from [https://github.com/VirtoCommerce/swagger-codegen](https://github.com/VirtoCommerce/swagger-codegen)

Open command prompt and navigate to the *swagger-codegen* folder.

Run “mvn clean package” command. This will build the *swagger-codegen* project (wait until the build completes).

Create the following batch file somewhere in your system and edit paths to your swagger codegen directory (**swagger_codegen_dir**),  swagger JSON URL (**swagger_url**) and the name of the C# project to be generated (**project_name**):

```
set swagger_codegen_dir=C:\swagger-codegen
set swagger_url=http://localhost/admin/docs/MyModuleId/v1
set project_name=MyModule.Client
set output_dir=%~dp0output
Â 
set additional_properties=packageName=%project_name%,excludeTests=true,targetFramework=v4.5.1,optionalSolutionFile=false,optionalSupportingFiles=false,sourceFolder=.
set system_properties=modelDocs=false,apiDocs=false,modelTests=false,apiTests=false
Â 
pushd "%swagger_codegen_dir%"
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate -i %swagger_url% -l csharp -o %output_dir% --additional-properties %additional_properties% -D %system_properties%
popd
```

As a result you will have the environment ready to build the API client. Run the **generate-client.bat** and check the **output** directory which will be created next to the batch file.

## Updating swagger-codegen

**The next steps are required only in case of swagger-codegen code was updated.** Skip this section and go to ******Updating *********API client*** section if you are building *swagger-codegen* for the first time or it wasn’t updated:

Update *swagger-codegen* from [https://github.com/VirtoCommerce/swagger-codegen](https://github.com/VirtoCommerce/swagger-codegen)Open command prompt

Run "mvn clean package" command

As a result you will have the *swagger-codegen* updated to the latest version and have the environment ready to build the API client.

## Updating API client

### Regenerating API client classes

Get the latest API source code (module)

Rebuild the module in order to update API

Open VC Manager **~\docs\<<VirtoCommerce module id>>\v1** in browser (e.g. [http://localhost/admin/docs/VirtoCommerce.Platform/v1](http://localhost/admin/docs/VirtoCommerce.Platform/v1))

Save (update the old one) API generated json from browser

Delete or rename the old generated ~\vc-client folder

Open command prompt and navigate to *swagger-codegen* folder (the *generate-vc-client.bat* must be there)

Run *generate-vc-client.bat*

As a result you will get the vc-client folder with the generated API client classes. Now you need to update the API client project with the new classes.

### Updating API client project

Open Total Commander (TC hereafter in the document)

On the left pane of TC navigate to the generated ~\vc-client\src\main\csharp\VirtoCommerce\Client folder

On the right pane of TC navigate to your API client project classes location

Select 3 folders (Api, Client, Model) in the left pane and execute Commands -> Synchronize dirs... command

![]()In the command view click “Compare” command

![]()  
The difference in files will be shown in the results area. Now you should decide which files should be updated in the API client library project.  
  
After you selected the changes to synchronize, click “Synchronize” button.Open your API client project and navigate to source files location

Ensure that “Show All Files” option is activated:

![]()  
  


Include all *.cs files that are not added to the project

Remove references to files that are no longer available (deleted during synchronization)

Build solution. Fix build errors, if any (most of the errors are caused by not all files being added or removed to/from the solution.

As a result you have an updated API client library.

## Updating nuget package

**The next steps are required only if you don’t use API client project directly and need to update the Nuget package.**

Open the solution containing your API client nuget package

Open ***<<your API Client>>****.nuspec*** file:  
![]()

 

Update the version of the Nuget package (it is recommended the Nuget package version to match the VirtoCommerce platform version)

Change the build option to “**Release**” and build the solution

Run the command in the PMC: nuget pack "**<path>/*****<<your API Client>>**.*csproj" -Symbols -Properties Configuration=Release

  * <path> - path to the project file.



Login to Nuget website with appropriate credentials

Go to “Upload package” tab

Click “Choose file”:  
![]()

 

Navigate to the **<<API Client folder>>\bin\Release**

Select the **<<API Client>>.<<version>>.nupkg** file

Click “Upload”

Check the package information after upload and confirm

Your API Client Nuget package has been updated. You can update it in your target solution using Visual Studio.

  

