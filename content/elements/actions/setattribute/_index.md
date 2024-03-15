---
title: "Setattribute"
menuTitle: ""
date: 2024-03-15T11:25:00+01:00
tags: []
---

### Description

Creates and sets an attribute value.

This action is useful when you need to dynamically create an attribute on some data node.

### Attributes

| Name  | Description                                   | 
|-------|-----------------------------------------------| 
| ref   | required reference to the parent element      |
| name  | required name of attribute                    |
| value | value of attribute defaulting to empty string |

## Events

| Name  | Description                                    |
|-------|------------------------------------------------|
| error | in case `ref` or `name` haven't been specified |

### Examples

* [setattribute]({{% siteparam "demoUrl" %}}actions/setattribute.html)
