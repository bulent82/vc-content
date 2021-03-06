---
title: Working with Platform Manager
layout: docs
date: 2015-11-25T14:55:28.893Z
permalink: /docs/vc2devguide/Working+with+Platform+Manager
---

## Virto Commerce Platform

We have isolated a clean platform constructed with full compliance with the principles of SOLID and DDD and oriented for use in Azure or IIS. It is based on the next stack of technologies:

* ASP.NET MVC (as web framework)


* ASP.NET Web API (REST-full web services)


* AngularJS (UI)


* Entity Framework with migrations (persistence layer)



The platform can be used for new module development or as a starting point for building your own application.

### Included functionality

* Single-page web application with horizontal scrolling blade-based navigation (AngularJS)


* HTML5 compatible UI theme


* Authentication and authorization (ASP.NET Identity)


* Users and roles management


* Module based extensibility


* Widget based UI extensibility


* Notificationss


* Background jobs execution and scheduling (Hangfire)


* Assets management


* Application settings management


* Caching with support for cache provider extensions



## Deployment

Virto Commerce Platform can be deployed to Microsoft Azure cloud or any other environment which has the following components installed:

* Microsoft .NET Framework 4.5.1


* Internet Information Services 7 or later


* Microsoft SQL Server 2008 or later


