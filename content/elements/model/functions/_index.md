---
title: "<fx-function>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, model, fx-function]
weight: 10

---

## Description

Allows to define custom inline function in either XPath/XQuery or Javascript.

## Attributes

| Name | Description |
|------|-------------|
|signature| the function signature. Must use 'local' prefix |
|type| can be 'text/javascript', 'text/xpath', 'text/xquery' or 'text/xquf' (XQuery Update Facility) |

## Events

none

## Examples

### Xquery Update Facility

```
<fx-function
        signature="update($element as element()) as element()*"
        type="text/xquf">
    copy $xml := $element modify (
    for $ref in $xml/element
    return insert node $ref/@name with $xml/element/name/text()
    ) return $xml
</fx-function>
```

### JavaScript

```
<fx-function signature="now() as xs:string" type="text/javascript">
    const now = new Date();
    return `${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}:${String(now.getSeconds()).padStart(2, '0')}`;
</fx-function>
```


* [Custom inline functions]({{% siteparam "demoUrl" %}}functions.html)
* [Randomizer]({{% siteparam "demoUrl" %}}randomizer.html)



