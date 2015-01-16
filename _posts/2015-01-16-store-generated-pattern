---
layout: post
title: "StoreGeneratedPattern Annotation (V3)"
description: ""
categories: [V3, Store Generated]
---

StoreGeneratedPattern is an attribute annotation (in V3 Protocol) on property of entity type, which can be applied to primitive property. The values are “None”, “Identity” and “Computed”, which indicates whether the property of entity needs a value during insert and update operation. The annotation in metadata will be shown as following:

```xml
<EntityType Name="Order">
    <Key>
        <PropertyRef Name="Id" />
    </Key>
    <Property Name="Id" Type="Edm.Int32" Nullable="false" annotation:StoreGeneratedPattern="Identity" />
    <Property Name="Name" Type="Edm.String" Nullable="false" />  
</EntityType>
```

There are two approaches to add StoreGeneratedPattern annotation on a primitive property:
Using DatabaseGenerated attribute:
```
public class Order
{
    [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
    public int Id { get; set; }

    public string Name { get; set; }
}
```

Using API call
```
ODataModelBuilder builder = new ODataModelBuilder();
builder.Entity<Order>().Property(c => c.Id).HasStoreGeneratedPattern(DatabaseGeneratedOption.Identity);
```
