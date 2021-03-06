---
title: Filters
layout: docs
date: 2015-09-04T21:43:54.507Z
permalink: /docs/vc2devguide/Filters
---

Filters are simple methods that modify the output of numbers, strings, variables and objects. They are placed within an output tag **{{****}}** and are separated with a pipe character **|**.

```
<-- product.title = "Sample Product Title" -->
{{ product.title | upcase }}
```

```
SAMPLE PRODUCT TITLE
```

In the example above, **product** is the object, **title** is its attribute, and **upcase** is the filter being applied.

 

Some filters require a parameter to be passed.

```
{{ product.title | remove: "Sample" }}
```

```
Product Title
```

 

Multiple filters can be used on the output. They are applied from left to right.

```
<-- product.title = "Sample Product Title" -->
{{ product.title | upcase | remove: "SAMPLE" }}
```

```
PRODUCT TITLE
```

## Creating your own filters

As a developer, you can create custom filters that then can be used by a themes designer.

Creating filters is very easy. Filters are just methods which take one parameter and return a modified string. You can use your own filters by passing an array of filter types to the Render, an example follows: template.Render(filters: new[] { typeof(MyTextFilters), typeof(MyDateFilters) });

 

```
public static class TextFilter
{
	public static string Textilize(string input)
	{
		return TextileFormatter.FormatString(input);
	}
}
```

you will then need to register the filter in the Virto Commerce frontend:

```
var filters = new[] { typeof(ModelFilters), typeof(TranslationFilter), typeof(TextFilter) };
```

A filter can access the current context if you add a Context object as the first argument to your filter method. DotLiquid will automatically pass the current context to your filter:

```
public static String MyFilter(Context context, String input)
{
//...
}
```

 

 


