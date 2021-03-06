---
title: Source Code Getting Started
layout: docs
date: 2016-07-28T07:41:47.177Z
permalink: /docs/vc2devguide/Source+Code+Getting+Started
---

## Summary

Use this guide to obtain source code and setup development environment.

## Contents



### Prerequisites

* Microsoft .NET Framework 4.5.1
* Internet Information Services 7 or later
* Microsoft SQL Server 2008 or later (Express or Full)
* Visual Studio 2013 or later

### Get source code

Download the latest source code from GitHub repository [https://github.com/VirtoCommerce/vc-platform](https://github.com/VirtoCommerce/vc-platform) by clicking the **Download ZIP** button.Extract all files.## Commerce Manager

### Build solution

Open **VirtoCommerce.Platform.sln** solution.In Solution Explorer window right-click on solution and select **Manage NuGet Packages for Solution**. In the opened window click the **Restore** button.  
![](../../assets/images/docs/image2016-7-26_11-23-32.png)Build the solution.### Configure SQL Server

SQL Server Authentication mode must be enabled.  
![](../../assets/images/docs/image2015-4-7_11-44-53.png) 

Create the new login named **virto** with password **virto**. The password policy enforcement should be switched off for a simple password like this.

```
USE master; CREATE LOGIN virto WITH PASSWORD = 'virto', CHECK_POLICY = OFF
```

Give the **CREATE ANY DATABASE** permission to user virto. This will allow you to create a database automatically when Commerce Manager starts. For new databases created with this permission the user will have the **db_owner** role while access will be denied for any other database.  


```
USE master; GRANT CREATE ANY DATABASE TO virto
```

In the **VirtoCommerce.Platform.Web** project open the **web.config** file and make sure the **VirtoCommerce** connection string has correct parameters for your configuration, particularly **Data Source** (SQL Server address), **Initial Catalog** (database name), **User ID** (user name) and **Password**.

### Configure IIS

Open **IIS Manager** and add new application to **Default Web Site** with alias **admin** and physical path to **VirtoCommerce.Platform.Web**. Select application pool which uses **.NET CLR Version 4.0** and **Integrated pipeline mode**.  
![](../../assets/images/docs/image2016-7-26_11-29-36.png)Inside the **admin** application add a new virtual directory with alias **Assets** and physical path to **VirtoCommerce.Platform.Web\App_Data\Assets**. If there is no Assets directory inside App_Data, create it.  
![](../../assets/images/docs/image2016-7-26_11-44-17.png)  
  
Your web site structure should be similar to the one shown below:  
![](../../assets/images/docs/image2016-7-26_12-8-20.png)### Configure file system

Open properties for the folder where you have extracted source code (vc-platform-master by default) and give permission **Read & execute** to **Users** group if this permission is not inherited from the parent folder.  
![](../../assets/images/docs/image2015-8-21_15-46-0.png) Open properties for **VirtoCommerce.Platform.Web\App_Data** folder and give permission **Modify** to **IIS_IUSRS** user group.  
![](../../assets/images/docs/image2015-9-23_11-29-42.png)Open properties for **VirtoCommerce.Platform.Web\Modules** folder and give permission **Modify** to **IIS_IUSRS** user group as shown above.### Start Commerce Manager

Open the [http://localhost/admin](http://localhost/admin) URL in browser. A sign in page should open:

![](../../assets/images/docs/image2015-2-26_12-5-39.png)

 

The default administrator account login is **admin** and the password is **store**.

## Next steps (optional)

The VC platform is up and running. What's next? Here are some ideas to try.

### Install some modules

#### Install modules in VC Manager app

Install some modules as described in [[Modules management]] tutorial.

#### Manual **module installation** from source code

Do you prefer the installation in **dev**eloper way? Great, follow these steps for each module:

Download the latest module source code from GitHub repository [https://github.com/VirtoCommerce/vc-module-*<<module name>>*](https://github.com/VirtoCommerce) by clicking the **Download ZIP** button.Extract it to platform's **Modules **directory. You also can extract it to any directory and link it to the Modules directory using **mklink /d** command.Open and compile module solution.Restart IIS.Open Manager app. The new module will be installed automatically. Check its status in ****C**onfiguration > Modules > Installed**.### Create your own module

Why not to **create your own** module? Follow the steps described in [[Developing a custom solution]] tutorial.

### How platform loads modules

![](../../assets/images/docs/VC_modules_copy_process.png)

 

 


