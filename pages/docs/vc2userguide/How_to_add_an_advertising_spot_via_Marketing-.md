---
title: How to add an advertising spot via Marketing?
layout: docs-user
date: 2016-02-03T13:53:58.500Z
permalink: docs/vc2userguide/How+to+add+an+advertising+spot+via+Marketing
---

# How to add an advertising spot via Marketing?

There are steps to prepare dynamic content infrastructure.

[[Create a content item.|Create a content item]][[Create a content placeholder.|Create a content placeholder]][[Create a content publishing.|Create a content publishing]]### Add content place to a page

There are steps to add a dynamic content to a website pageOpen a website page html file.Insert code to your Html, where Id is  placeholder name<vc-content-place id="Right banner 240x400" class="col-sm-4 col-md-4 rightblock"></vc-content-place>

### Add real advertising content

Go to Marketing module.Select "Dynamic content" in the module blade.Select "Content items" in the opening blade.Select content item to apply with new content. It is "Google adv 200x240" in [[Create a content item]] example.Insert into Html google ads snippet:<script async src="//[pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script]()>  
<!-- Gift -->  
<ins class="adsbygoogle"  
 style="display:inline-block;width:240px;height:400px"  
 data-ad-client="ca-pub-7764700480965053"  
 data-ad-slot="9634585522"></ins>  
<script>  
(adsbygoogle = window.adsbygoogle || []).push({});  
</script>

![](../../assets/images/docs/image2016-2-3_15-51-23.png)

6. Save changes.

 New content will allow immediately on your website page.


