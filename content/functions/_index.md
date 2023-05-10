---
title : "Functions"
date : 2022-06-03T10:42:31+01:00
chapter : true
tags: ["Version 1.0.0", functions]
---

# Functions

This chapter describes the builtin functions of Fore. As Fore uses
<a href="https://www.w3.org/TR/xpath-functions-31/" target="_blank">XPath 3.1</a> as its expression language you also have access to the large
library of functions that are defined by the standard.  

* <a href="https://maxtoroq.github.io/xpath-ref/" target="_blank">XPath 3 function reference</a>

> Not 100% of the XPath 3.1 functions are available in fontoXPath. There are a few that might not be (fully)
> implemented. In doubt please refer to their <a href="https://github.com/FontoXML/fontoxpath" target="_blank">github page</a> or 
> test in their wonderful <a href="https://xpath.playground.fontoxml.com/" target="_blank">fontoXPath playground</a>.

In addition to XPath Fore defines some built-in functions that are essential for building fully event-driven user-interfaces.

## `base64encode(string)`

This is probably the least used function but sometimes you need to base64-encode a string e.g. for sending it
as a GET param. 

Param:
* required: `string` - a string to be encoded

Returns:
* base64Encoded string

## `context(id)`

The `context()` function is needed in situations where several instance data sources are involved.

Param:
* optional: 'id' - an id of an element to use as context. If not given returns the parent context of the current context.

## `event(property)`

The `event` function is essential when working with events and params need to be passed. It allows to access properties
of the event details object which is passed in by the event dispatcher.

Param:
* required: property - a property of the event details object by name

Returns:
* value of the respective property. Might be a string, object or nodes depending on event type

> `event` is often used in conjunction with `fx-dispatch` action which allows to set properties of a custom event.

## `index(id)`

The `index` function is used in combination with `fx-repeat` elements. It returns the current index of a given repeat.

Param:
* required: id - the id of an `fx-repeat` element

Returns:
* an integer denoting the currently active repeat item

## `instance(id)`

The `instance` function is the most important function. It allows to address a certain `fx-instance` element for data-binding.

Param:
* optional: id - when given must point to an existing `fx-instance` element with given id. If not given it will default the first `fx-instance` element in document order

Returns:
* the root context for matching `fx-instance` element. The type of the root context depends on the type of instance which can currently be 'xml' or 'json'. For XML the root node of the instance data is returned. For JSON the outermost map or array will be returned.

## `log(id)`

The `log` function is just for development purposes and can be used to log some instance data to the document.

Param:
* required: id - the id of the instance to log

Returns:
* renders instance data to the document. 

Should output it's content to a `<code>` block.

```
<code>{log('default')}</code>
```