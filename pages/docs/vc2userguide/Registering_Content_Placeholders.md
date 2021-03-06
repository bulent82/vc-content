---
title: Registering Content Placeholders
layout: docs-user
date: 2015-11-12T07:30:23.533Z
permalink: docs/vc2userguide/Registering+Content+Placeholders
---

# Registering Content Placeholders

### Introduction

Content Placeholders must be registered in VirtoCommerce platform manager  and in Storefront theme template before Dynamic Content can be delivered within them. By default, the Content Placeholders provided with VirtoCommerce are already registered. However, if you add new or rename existing Content Places, you will need to register them following the steps below. Remember, you only need to register a Content Place once. Once registered, the Content Place becomes available for assignment to multiple pieces of Dynamic Content.

<div class="note">
	Your user account must have the Manage Content Places granted permission to perform these tasks in VirtoCommerce administration application.
</div>

### Register dynamic content place in strorefront theme template

To register dynamic content placeholder in storefront theme template only need add folow line 

```
<div data-vccontentid="Placeholder identity here"></div>
```

You can do it by two ways 

1. In manager UI Content->Themes->Edit Css/HTML
2. Manual in Storefront/App_Data/Themes/{{Store theme name}}

In manager UI Content->Themes->Edit Css/HTMLManual in Storefront/App_Data/Themes/{{Store theme name}} 

### Register dynamic content place in manager

1. Open **Marketing **module
2. Select **Dynamic Content**
2. Go to *Content Placeholders* 
3. Click **ADD** button

![](../../assets/images/docs/image2015-6-4_11-11-41.png)

4. In the wizard blade set Name, Description fields.

![](../../assets/images/docs/image2015-6-4_11-12-15.png)

Name should match the area name in the page template created by the web developer.

In the description field you can provide some additional information on the content placeholder e.g. Width/Height to support marketers with additional information while they create Dynamic Content for the Content Placeholder.

Also you can add default image for the placeholder.

5. Click **Create **button.

The created Content Placeholder will be added to the list and can be used for Dynamic Content displaying.

### Editing Content Placeholder

Open **Marketing **module.Select *Dynamic content*.Select *Content Places*.Click the selected Content Placeholder or click it and click **EDIT** button in the toolbar above the list.Edit the required fields.Save changes.### Deleting Content Places

Open **Marketing **module.Select *Dynamic content*.Select *Content Placeholders*.Select Content Placeholder you want to delete.Click **DELETE **button in the blade of the placeholder.Confirm deletion.**Note:***Content Placeholders can be easily deleted even if they are used in any registered Content Publishing. The only conciquence of this is that the Content Publishing won't be available while evaluating Dynamic Content for that area.*


