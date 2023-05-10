---
title: "Concepts & Terms"
menuTitle: "Concepts & Terms"
date: 2023-05-09T19:22:22+02:00
tags: []
---


## Scoped Resolution

'Scoped Resolution' takes place whenever `ref` attributes are resolved. It allows
to use relative binding expressions that are resolved upwards the document tree.

It is a similar concept as with usual relative linking in HTML or navigating a directory-structure.

An example illustrates this best:
```
<fx-instance>
    <data>
        <address>
            <name>Alice</name>
        <address>
    </data>
</fx-instance>
<fx-bind ref="address">
    <!-- scoped resolution happens here -->
    <fx-bind ref="name"></fx-bind>
<fx-bind>
```

When the nested `fx-bind` element is found it will resolve the tree upwards until it reaches the `fx-fore` element. 
While climbing upwards each `ref` attribute that is found will be picked up to build a complete absolute expression from it.

For the example it will resolve to `address/name` and return the 
node which has the value 'Alice' here.

The `instance()` function without arguments return us the default instance which is 
always the first in document order.

> Please note that you never need to spell out the root node when refering to a data item. So just `address` instead of
> `data/address`. 

 
