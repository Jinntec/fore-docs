---
title: "Concepts & Terms"
menuTitle: "Concepts & Terms"
date: 2023-05-09T19:22:22+02:00
tags: []
---

## Binding Expression

A binding expression is represented in markup as a `ref` or `data-ref` attribute. The expression language is XPath 3 which allows for complex
bindings that include filters with function calls, conditional etc.

Binding Expressions are relative to their parent bindings - see under 'Scoped Resolution'.

## Id Resolution

As Fore offers repeating sections via `fx-repeat` or `data-ref` there will be the situation that
`id` attributes present in the template of a repeat get duplicated at runtime.

For example:
```
<fx-repeat ref="items">
  <template>
     <div id="myDiv">....</div>
  </template>
</fx-repeat>
```

This will result in as many `<div>` elements with id `myDiv` as you got items in your data.

To avoid clashes Fore implements an Ìd Resolution` algorithm to make sure that you can still refer to the right repeated
element.

Example:
```
<fx-repeat ref="items">
    <template>
        ...
        <div id="myId-">
        ...
        <!-- dispatch 'hello' event to 'myId' -->
        <fx-dispatch name="hello" targetid="myId"></fx-dispatch>
    </template>
</fx-repeat>

<!-- rolled out at runtime -->
<fx-repeat ref="items">
    <fx-repeatitem>
        <div id="myId">
        ...
        <fx-dispatch name="hello" targetid="myId"></fx-dispatch>
    <fx-repeatitem>
    <fx-repeatitem>
        <div id="myId">
        ...
        <fx-dispatch name="hello" targetid="myId"></fx-dispatch>
    <fx-repeatitem>
    <fx-repeatitem>
        <div id="myId">
        ...
        <fx-dispatch name="hello" targetid="myId"></fx-dispatch>
    <fx-repeatitem>
```
Here the dispatch action refers to an id - Id Resolution will make sure that the id resolves within the context of the enclosing repeat item. This works also for nested repeats.


## Scoped Resolution

'Scoped Resolution' takes place whenever `ref` or `data-ref` attributes are resolved. It allows
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

 
