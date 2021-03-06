---
title: Creating new tax provider
layout: docs
date: 2015-10-16T06:12:28.163Z
permalink: /docs/vc2devguide/Creating+new+tax+provider
---

In order to calculate taxes in Virto Commerce you must register at least one TaxProvider implementation. Fixed rate tax provider already implemented in Virto Commerce 2.x. We recommend you read [creating new module](http://docs.virtocommerce.com/display/vc2devguide/Creating+New+Module)  before you start implementing a new tax provider. The article will walk though the required steps for creating a module and extending the system with a new tax provider.

## Define new tax provider

Create new module ([creating new module](http://docs.virtocommerce.com/display/vc2devguide/Creating+New+Module)).Create a class which should be derived from TaxProvider abstract class and override CalculateRate method. When Virto Commerce 2.x calculates tax rates the CalculateRate methods of your class will be called.Register in system and define settings.Register your module class in the IoC container. This must be done in PostInitialize method in your module class. You can also define all needed settings which will be used in your method and can be changed in the management UI. You may define tax provider settings as module settings in the module manifest file ([manage module setting](http://docs.virtocommerce.com/display/vc2devguide/Managing+Module+Settings)) and you can pass the module settings to a tax provider constructor in registration.  
  
```
var settingManager = _container.Resolve<ISettingsManager>();
taxService.RegisterTaxProvider(() => new FixedTaxRateProvider(moduleSettings.First(x => x.Name == "VirtoCommerce.Core.FixedTaxRateProvider.Rate"))
	{
    	Name = "fixed tax rate",
        Description = "Fixed percent tax rate",
        LogoUrl = "http://virtocommerce.com/Content/images/logo.jpg"
    });
```

All settings may have default values that can be used for default methods if not overridden by custom values later.

  


You may see examples on how to define and register new tax provider in the current solution: (VirtoCommerce.CoreModule - FixedTaxRateProvider)

## Enable and configure tax provider for store

After your module is installed in your target system, all your tax providers should appear and be available for configuration in every store in your system under Store->Tax providers widget. You can configure tax provider settings for each store individually:

* enable/disable method for current store


* edit all settings and what you define for the tax calculation provider


* use a custom UI for a more detailed tax provider configuration



After you complete the configuration, your tax provider will be used for tax calculation of orders in the store.

## Management UI customization

If a standard user interface is not enough, then consider implementing your own UI for managing tax providers through the standard UI extension point (widget container with group ”taxProviderDetail”). You can read more about extending the existing UI with widgets [[here|Widgets]].

## Related articles

Related articles appear here based on the labels you select. Click to edit the macro and add or change labels.




