---
title : "Functions"
date : 2022-06-03T10:42:31+01:00
chapter : true
tags: [functions]
weight: 60
---

# Functions

An overview of all functions available in Fore.

## XPath Functions
As Fore uses
<a href="https://www.w3.org/TR/xpath-functions-31/" target="_blank">XPath 3.1</a> as its expression language you also have access to the large
library of functions that are defined by the standard.  

* <a href="https://maxtoroq.github.io/xpath-ref/" target="_blank">XPath 3 function reference</a>

> Not 100% of the XPath 3.1 functions are available in fontoXPath. There are a few that might not be (fully)
> implemented. In doubt please refer to their <a href="https://github.com/FontoXML/fontoxpath" target="_blank">github page</a> or 
> test in their wonderful <a href="https://xpath.playground.fontoxml.com/" target="_blank">fontoXPath playground</a>.

In addition to XPath Fore defines some built-in functions that are essential for building fully event-driven user-interfaces.

## Fore Functions
### `base64encode(string)`

This is probably the least used function but sometimes you need to base64-encode a string e.g. for sending it
as a GET param. 

Param:
* required: `string` - a string to be encoded

Returns:
* base64Encoded string

### `context(id)`

The `context()` function is needed in situations where several instance data sources are involved.

Param:
* optional: 'id' - an id of an element to use as context. If not given returns the parent context of the current context.

### `event(property)`

The `event` function is essential when working with events and params need to be passed. It allows to access properties
of the event details object which is passed in by the event dispatcher.

Param:
* required: property - a property of the event details object by name

Returns:
* value of the respective property. Might be a string, object or nodes depending on event type

> `event` is often used in conjunction with `fx-dispatch` action which allows to set properties of a custom event.

### `fore-attr(attribute-name)`

Returns the value of an attribute on the `fx-fore` element in scope. Can be used to pass values to a Fore page loaded via
the `src` attribute which in turn can use these values inside of its logic with the help of this function.

Param:
* required: attribute name - an attribute name present on the Fore element in scope

Returns:
* the value of the attribute

### `index(id)`

The `index` function is used in combination with `fx-repeat` elements. It returns the current index of a given repeat.

Param:
* required: id - the id of an `fx-repeat` element

Returns:
* an integer denoting the currently active repeat item

### `instance(id)`

The `instance` function is the most important function. It allows to address a certain `fx-instance` element for data-binding.

Param:
* optional: id - when given must point to an existing `fx-instance` element with given id. If not given it will default the first `fx-instance` element in document order

Returns:
* the root context for matching `fx-instance` element. The type of the root context depends on the type of instance which can currently be 'xml' or 'json'. For XML the root node of the instance data is returned. For JSON the outermost map or array will be returned.

### `local-date()`

Returns local date

Example output: `18/12)2023`

### `local-dateTime()`

Returns local dateTime

Example output: `18/12/2023, 17:01:56`

### `log(id)`

The `log` function is just for development purposes and can be used to log some instance data to the document.

Param:
* required: id - the id of the instance to log

Returns:
* renders instance data to the document. 

Outputs it's content to a `<code>` block.

```
<code>{log('default')}</code>
```

### `uri()`

Returns the full URI from the browser

Example output: `http://localhost:8090/demo/uri.html?param1=value1&param2=value2#hash`

### `uri-fragment()`

Returns the fragment of the current URI

Example output: `#hash`


### `uri-query()`

Returns the query part of the URI

Example output: `?param1=value1&param2=value2`

### `uri-param(param-name)`

Returns the value for URI param given by argument

Example output: `value1`

### `uri-path()`

Returns the path part of the current URI

Example output: `/demo/uri.html`

### `uri-port()`

Returns the port of the current URI

Example output: `8090`

### `uri-scheme()`

Returns the URI scheme of the current page

Example output: `http:`

### `uri-scheme-specific-part()`

Returns the URI without the scheme-specific part

Example output: `//localhost:8090/demo/uri.html?param1=value1&param2=value2#hash`




