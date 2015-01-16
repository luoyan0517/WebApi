---
layout: post
title: "Relax Flag for Version Constraint (V3 & V4)"
description: ""
category: edm model builder
---

For both WebAPI OData V3 and V4, a flag IsRelaxedMatch is introduced to relax the version constraint. With IsRelaxedMatch = true, ODataVersionConstraint will allow OData request to contain both V3 and V4 max version headers (V3: MaxDataServiceVersion, V4: OData-MaxVersion). Otherwise, the service will return response with status code 400. The default value of IsRelaxdMatch is false.

{% highlight csharp %}
public class ODataVersionConstraint : IHttpRouteConstraint
{
  ......
  public bool IsRelaxedMatch { get; set; }
  ......
}
{% endhighlight %}

To set this flag, API HasRelaxedODataVersionConstraint() under ODataRoute can be used as following:
{% highlight csharp %}
ODataRoute odataRoute = new ODataRoute(routePrefix: null, pathConstraint: null).HasRelaxedODataVersionConstraint();
{% endhighlight %}
