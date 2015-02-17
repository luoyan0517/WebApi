---
layout: post
title: "String function parameter issue"
description: ""
category: Work around
---

Supposed you build an OData function with a string parameter, for example

{% highlight csharp %}

var builder = new ODataConventionModelBuilder();
builder.EntityType<Customer>().Function("MyFunction").Parameter<string>("p).Returns<int>();
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

Then you invoke this function using the following parameter:

1. ~/Customers(1)/Default.MyFunction(p='112')
2. ~/Customers(1)/Default.MyFunction(p='112a')
3. ~/Customers(1)/Default.MyFunction(p='a112')

You will get wrong parameter value in the MyFunction() method in the controller. 

The workaround so far is to remove the [FromODataUri] attribute from MyFunction() in the controller. 

Thanks.

