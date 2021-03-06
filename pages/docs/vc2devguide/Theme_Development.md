---
title: Theme Development
layout: docs
date: 2016-05-31T12:02:37.970Z
permalink: /docs/vc2devguide/Theme+Development
---

# Getting Started

Whenever you are building theme for your client or yourself this guide will provide instructions on how to create a theme.

There are several ways how the theme can be developed. First you can start of with one of the sample themes provided with a product or download one from our [appstore](http://virtocommerce.com/appstore) or get on from [Shopify themes](https://themes.shopify.com/) as these themes are fully supported. You can then edit that theme using two basic methods:

Edit theme using admin tool by going to "***Browse->Content->Edit CSS/HTML***", orby using Visual Studio, simply open the the frontend solution and start editing files located under "App_data/themes/{name of the theme}" inside VirtoCommerce.Website project (make sure to enable show all files in the top toolbar of solution explorer to be able to see the files). The files you edit here won't be overwritten when website is running.You can also use the hybrid approach by editing files in both backend and using Visual Studio or in fact any other editor. The last saved file will be used (note: when editing a file in the Commerce Manager, the changes will overwrite an older file).

## Liquid Reference

Liquid is the templating engine that powers Virto Commerce templates. Go to [[Liquid Documentation|Liquid Reference]].


