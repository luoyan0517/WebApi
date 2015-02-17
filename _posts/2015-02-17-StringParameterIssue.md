---
layout: post
title: "String function parameter issue"
description: ""
category: Work around
---

Supposed you build an OData function with a string parameter, for example

{% highlight csharp %}

var builder = new ODataConventionModelBuilder();
builder.EntityType<Customer>().Function("MyFunction").Parameter<string>("p").Returns<int>();
return builder.GetEdmModel();

{% endhighlight %}

And you create the method in controller:

{% highlight csharp %}
public class CustomersController : ODataController
{
    [HttpGet]
    public int MyFunction(int key, [FromODataUri]string p)
    {
        ... 
    }
}
{% endhighlight %}

Then you invoke this function using the following parameters:

1. ~/Customers(1)/Default.MyFunction(p='113')
2. ~/Customers(1)/Default.MyFunction(p='114a')
3. ~/Customers(1)/Default.MyFunction(p='a115')

You will get the following parameter value in the MyFunction() method in the controller as:

{% highlight csharp %}
1. public int MyFunction(1, 113)
2. public int MyFunction(1, 114)  // wrong value
3. public int MyFunction(1, null) // wrong value

{% endhighlight %}


The workaround so far is to remove the [FromODataUri] attribute from MyFunction() in the controller. And, it's only for integer-starting string.

Thanks.

