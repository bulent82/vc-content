---
title: Mobile Starter kit. Getting started
layout: docs-dev
date: 2016-08-17T09:31:01.713Z
permalink: docs/vc2devguide/Mobile+Starter+kit.+Getting+started
---

## Summary

Use this guide to setup development environment for Virto Commerce Mobile Starter kit and showcasing it publicly.

## Contents



## Prerequisites

### Visual Studio 2015 configuration

Required VS2015 compenents are not installed by "typical installation". Run VS2015 installer and make sure **Cross Platform Mobile Development** > **HTML/JavaScript** component is installed.

### Ionic command line utility (CLI)

[Install the Ionic CLI](http://ionicframework.com/docs/cli/install.html):

```
npm install -g ionic
```

## Getting source code

The Virto Commerce Mobile Starter kit source code is currently available to partners and customers only. Contact us for more info on how to get the mobile starter kit: [https://virtocommerce.com/contact-us](https://virtocommerce.com/contact-us).

## Develop with Starter kit

Open the **VirtoCommerce.Mobile.sln** solution. (VS2015 should restore the required npm and bower packages in background automatically).**Serve** the app for testing: Go to the root directory of Mobile Starter kit source code in command prompt. Type:

```
ionic serve --lab
```

The site [http://localhost:8100/ionic-lab](http://localhost:8100/ionic-lab) opens in browser with iOS and Android devices emulated.

Check and test the app running:

![](../../assets/images/docs/image2016-1-26_18-49-26.png)

  


Can minimize, but don't close the command prompt.Start modifying source code files under www folder. All updates to html and js will be automatically synchronized in browser.  
  
**Note:** The project is preconfigured to use demo data from [http://demo.virtocommerce.com](http://demo.virtocommerce.com/). You can switch to any other Virto Commerce Platform data source by changing the [Ionic CLI service proxy](http://ionicframework.com/docs/cli/test.html) in the project file. (Don't forget to point to storefront REST API url like [http://demo.virtocommerce.com/storefrontapi](http://demo.virtocommerce.com/admin/api)).

[Setting Virto Commerce Platform](http://docs.virtocommerce.com/display/vc2devguide/Source+Code+Getting+Started) locally.

## Showcase your app to everyone

The simplest and quickest way to showcase your new point of sale app is to publish it on [Ionic View](http://view.ionic.io/). Step-by-step guide on uploading and viewing an app with Ionic View: [http://ionicframework.com/docs/cli/uploading_viewing.html](http://ionicframework.com/docs/cli/uploading_viewing.html).

## Check out Mobile Starter kit app in action

A preconfigured Mobile Starter kit app is already available for your testing at Ionic View. Check for instructions at our [[Mobile Starter app]] page.

 

 

 


