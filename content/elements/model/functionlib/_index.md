---
title: "<fx-functionlib>"
menuTitle: ""
date: 2024-05-29T15:24:38+02:00
tags: []
weight: 12

---

## Description

The `fx-functionlib` elements allows to externalize collections of custom functions into a separate JavaScript file or embed them into an HTML page for re-use in other contexts.

When using a HTML page a functionlib can not only host the functions but at the same time document the
functions in the page.

However for security reasons it's preferrable to externalize JavaScript functions in `.js` files and it allows to use a debugger for the functions themselves, which can be a big help for development. 

## Attributes
| Name | Description                                    |
|------|------------------------------------------------|
| src | required attribute pointing to the url to load |
| prefix | The optional prefix allows to register all functions of a lib with a prefix to avoid name conflicts with other libraries or pre-existing functions.
 |


## Writing external JavaScript functions

To allow automatic registration of functions, these have to be made available as named module exports (ES6 syntax) in one of the ways shown in [lib1]({{% siteparam "demoUrl" %}}function-lib/lib1.js). 

For a JavaScript extension function this would look like this:
```
export function hello(message) {
    return 'Hello ' + message;
}
hello.signature = 'hello($message as xs:string) as xs:string';
```

(Example taken from lib1.js).

## Writing external XPath (XQuery, XQUF) functions
```
export const helloXPath = {
    signature: "helloXPath($who as xs:string) as xs:string",
    type: "text/xpath",
    functionBody: "concat('Hello - ', $who)"
};
```
## Export as named functions 

This line must always be at the end of the file finally exporting an array of functions that will be registered. 

```
export const functions = [theanswer, hello, helloXPath];
```


### Examples

* [function-lib]({{% siteparam "demoUrl" %}}function-lib/function-lib.html)
* [function-lib2]({{% siteparam "demoUrl" %}}function-lib/function-lib2.html)
* [randomizer]({{% siteparam "demoUrl" %}}randomizer.html)
