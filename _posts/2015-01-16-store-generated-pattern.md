---
layout: post
title: "StoreGeneratedPattern Annotation (V3)"
description: ""
categories: edm model builder
---

StoreGeneratedPattern is an attribute annotation (in V3 Protocol) on property of entity type, which can be applied to primitive property. The values are “None”, “Identity” and “Computed”, which indicates whether the property of entity needs a value during insert and update operation. The annotation in metadata will be shown as following:

{% highlight xml %}
<EntityType Name="Order">
    <Key>
        <PropertyRef Name="Id" />
    </Key>
    <Property Name="Id" Type="Edm.Int32" Nullable="false" annotation:StoreGeneratedPattern="Identity" />
    <Property Name="Name" Type="Edm.String" Nullable="false" />  
</EntityType>
{% endhighlight %}

There are two approaches to add StoreGeneratedPattern annotation on a primitive property:
Using DatabaseGenerated attribute:

{% highlight csharp %}
public class Order
{
    [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
    public int Id { get; set; }

    public string Name { get; set; }
}
{% endhighlight %}

Using API call

{% highlight csharp %}
ODataModelBuilder builder = new ODataModelBuilder();
builder.Entity<Order>().Property(c => c.Id).HasStoreGeneratedPattern(DatabaseGeneratedOption.Identity);
{% endhighlight %}
