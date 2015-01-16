---
title : "Case Insensitive, Unqualified function call & Enum prefix free"
layout: post
category: OData Parser Extension
---

Let's show how to expand the default OData Uri Parser behaviour:

### Basic Case Insensitive Support
User can configure as below to support basic case-insensitive parser behaviour.

{% highlight csharp %}
HttpConfiguration config = …
config.EnableCaseInsensitive(true);
config.MapODataServiceRoute("odata", "odata", edmModel);
{% endhighlight %}
**Note**: Case insensitive flag enable both for metadata and key-words, not only on path segment, but also on query option.
For example:

* ~/odata/$metaDaTa
* ~/odata/cusTomers
...

### Unqualified function/action call
User can configure as below to support basic unqualified function/action call. 

{% highlight csharp %}
HttpConfiguration config = …
config.EnableUnqualifiedNameCall(true);
config.MapODataServiceRoute("odata", "odata", edmModel);
{% endhighlight %}

For example:

Original call:
~/odata/Customers(112)/Default.GetOrdersCount(factor=1)

Now, you can call as:
~/odata/Customers(112)/GetOrdersCount(factor=1)

#### Enum prefix free
User can configure as below to support basic string as enum parser behaviour.

{% highlight csharp %}
HttpConfiguration config = …
config.EnableEnumPrefixFree(true);
config.MapODataServiceRoute("odata", "odata", edmModel);
{% endhighlight %}

For example:

Origin call:
~/odata/Customers/Default.BoundFuncWithEnumParameters(SimpleEnum=1,FlagsEnum=One, Four)

Now, you can call as:
~/odata/Customers/Default.BoundFuncWithEnumParameters(SimpleEnum='1', FlagsEnum='One, Four')

#### Advance Usage

User can do as below to support case insensitive & unqualified function call & Enum Prefix free:

{% highlight csharp %}
config.EnableCaseInsensitive(true);
config. EnableUnqualifiedNameCall (true);
config. EnableEnumPrefixFree (true);

config.MapODataServiceRoute("odata", "odata", edmModel);
{% endhighlight %}

Thanks.
