---
title: Extending Functionality
layout: docs
date: 2016-09-07T09:51:26.077Z
permalink: /docs/vc2devguide/Extending+Functionality
---

Virto Commerce Platform is an ASP.NET MVC and [AngularJS](http://angularjs.org/) Single Page Application with VirtoCommerce's modularity feature.

A module is a subdirectory of **~/Modules** directory which contains a **module.manifest** file. Additionally, a module can contain any other content such as JavaScript, CSS, image files, .NET assemblies, etc. Some content is specialized and specifics should be outlined in the module manifest. If a module contains .NET assemblies it is called a **managed module**.

Modules can extend Virto Commerce Platform either with JavaScript or with managed code.

JavaSript allows the user to:

* add new items to main menu. [[Registration in application's menu|Creating new module#registrationinapplication'smenu]][]()[]()
* add new widgets to widget containers (on dashboard or in blades). [Working with widgets](http://docs.virtocommerce.com/x/oQDr)
* add new blades
* add custom content inside the blade or totally redefine the content using [[metaform|Metaform]] control
* add new buttons and other content to existing blade toolbars. [Working with blade toolbar](http://docs.virtocommerce.com/x/DQHr)
* define new types of notifications and add new notification templates. [Working with notifications](http://docs.virtocommerce.com/x/TADr)
* define new UI for settings management

Managed code allows the user to:

* add new Web API controllers
* add new services
* override existing services
* modify database

The UI can be extended with Javascript and the backend can be extended with managed code.

In addition, new security permissions as well as new application settings are added with the module manifest, but they are still used either in JavaScript or in managed code.

In this tutorial you will learn how to create custom modules with and without managed code. Each module will be loaded to the main application and will have its entry in the main menu.


