---
title: Liquid Reference
layout: docs
date: 2015-09-17T08:50:25.393Z
permalink: /docs/vc2devguide/Liquid+Reference
---

DotLiquid is a templating system ported to the .net framework from Ruby’s [Liquid Markup](http://www.liquidmarkup.org/). You can have your users build their own templates without affecting your server security in any way.

Liquid utilizes tags, objects, and filters to load content. Each theme consists of .liquid files that contain tags, objects and filters.

  


### Tags

Tags are used to control the logic inside templates

```
<ul>
    {% raw %}
    {% for product in products %}
    <li>{{ product.title }}</li>
    {% endfor %}
    {% endraw %}
</ul>
```

[[Read more|Tags]]

### Objects

Object contain properties that can be displayed inside templates

```
{{ product.title }} <!-- Output: My Product Title -->
```

[[Read more|Objects]] 

### Filters

Filters are used to transform output of strings and objects

```
{{ product.title | upcase }} <!-- Output: MY PRODUCT TITLE -->
```

[[Read more|Filters]]


