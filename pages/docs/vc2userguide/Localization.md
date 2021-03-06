---
title: Localization
layout: docs-user
date: 2015-12-18T15:39:11.717Z
permalink: docs/vc2userguide/Localization
---

# Localization

## Summary

This article is about Virto Commerce Manager localization. The localization is based on resources (translation files) and translation implementation.

## Contents


## What is a translation file?

## File name pattern

The file name must match the *{lang}.{name}.json *pattern, where: 

* {lang} part is the ISO 639-1 two-letter language code;
* {name} is unique name throughout all Manager’s modules. The best decision here would be using module ID as the name.

## File format

For the sake of simplicity, we can consider that the translation file consists of **ID:Value**pairs, where **ID** is a unique key and **Value** is the translated text. The actual translation data structure is [JSON](https://en.wikipedia.org/wiki/JSON). 

```
{
  "cart.main-menu-title": "Shopping carts",
  "cart.blades.carts-list.title": "Shopping carts",
  "cart.blades.carts-list.labels.customer": "Customer",
  "cart.blades.carts-list.labels.items-count": "Items count",
  .... 
} 
```

*Sample localization file looking as simple key-value pairs.*

 

You can organize your translations by enclosing them inside namespaces. Structured JSON objects are created in this case. This is especially useful feature for heavy modules with many localized resources and Virto Commerce translation files are structured in this way.

```
{
  "cart": {
    "main-menu-title": "Shopping carts",
    "blades": {
      "carts-list": {
        "title": "Shopping carts",
        "labels": {
          "customer": "Customer",
          "items-count": "Items count"
        }
      },
      ....
} 
```

**Structured *Virto Commerce localization data.*

 

The unique ID for the translation text would be the path to the JSON object key separated by dots. E.g., in the above sample the ID to the "items-count" translation is "cart.blades.carts-list.labels.items-count". As you can see these two last samples represent the same IDs and are equivalent.

# **Where can I get ****additional translations for ****Virto Commerce?**

Virto Commerce keeps additional translations in a dedicated git repository: [vc-localization](https://github.com/VirtoCommerce/vc-localization). We’re asking and encouraging everyone to help us and translate our modules to as many languages as possible! 

# **How to translate to a new language?**

Selected modules or platform parts can be translated separately and independently. It takes 5 simple steps to create a new translation:

Download translations from a dedicated git repository ([vc-localization](https://github.com/VirtoCommerce/vc-localization));Choose source language (e.g. English);Clone the source language's translation files;

Replace language code from source to translated language code for each cloned translation file;

Translate the inner resources using any editor or specialized tools like[ poeditor](https://poeditor.com/),[ crowdin](https://crowdin.com/),[ getlocalization](https://github.com/VirtoCommerce/vc-localization/blob/master/www.getlocalization.com), etc.

# ****How to add translations to Virto Commerce Manager?****

 In order to add a translation, you just have to copy the translation files to "*App_Data\Localizations*" sub folder in your Virto Commerce Manager web application.

![](../../assets/images/docs/worddavfcad84194beb5713ec58287f9083a4ac.png)

**Note:** There is no limitation on the number of translation files, nor inner sub folders' structure.

# **Where can I find more technical information?**

More technical information and implementation details are available in [[Localization implementation]].

 


