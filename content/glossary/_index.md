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

## Default Instance

The 'default instance' in Fore is always the first in document order within a given `fx-fore` element. It will get an `id="default"` 
being set if no `id` attribute exists. The default instance can be either accessed by the `instance()` function without passing an argument or by `instance('default').

The `instance()` function can be omitted in binding expressions if there's no non-default instance in scope. 

The concept of a default instance allows to write binding expressions without explicitly naming the instance like e.g. `mypath/child` which will be equivalent to write `instance()/mypath/child` or `instance('default')/mypath/child`. As such it is mainly a convenience to reduce typing when accessing the first instance in document order.

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

## ForeBody

A 'ForeBody' means a `fx-fore` element including all of its content and it just a name picked for easier
referral when talking about Fore. 

## <a id="lazyinstance">Lazy Instance</a>

Lazily created data structure created from bindings in the UI.

See 'Lazy Mode'.

## Lazy Mode

In lazy mode the user does not need to specify a `fx-model` explicitly. 
When no `fx-model` is found at init time, Fore switches to lazy mode and creates a default data structure from the bindings found in the UI.

Example:
```
<fx-fore>
  <fx-control ref="forename">
    <label>Forename</label>
  </fx-control>
  <fx-control ref="lastname">
    <label>Lastname</label>
  </fx-control>
</fx-fore>
```
In this case Fore will come up with an auto-generated model and data structure looking like this:

```
<fx-fore>
  <fx-model>
    <fx-instance>
      <data>
        <forename></forename>
        <lastname></lastname>
      </data>
    </fx-instance>
  </fx-model>
  <fx-control ref="forename">
    <label>Forename</label>
  </fx-control>
  <fx-control ref="lastname">
    <label>Lastname</label>
  </fx-control>
<fx-fore>
```

Lazy mode is meant to be used for quick prototyping and very simple use cases. They do not allow to use binding facets or explicit submisssions.


## Relevance Selection

Relevance is a powerful features that comes into play in several places:
### Bound UI Elements

UI Elements can be bound by their `ref` attribute. If a `ref` expresssion does not point to a data item it becomes 'nonrelevant' which means:
* it's not shown to the User
* the elements' states (like 'readonly', 'required', 'valid'...) won't be updated unless a data item becomes available

This can be used hide/show complete sections in the UI depending directly on existence of a node. Once a bound node becomes available the
respective UI container or control will be shown.

### When sending a request

Whenever data are send, the RelevanceSelector will first filter all data items according to the relevance mode for that request.

By default all data items being nonrelevant will be filtered out before sending the data over the wire. During this filtering also empty
attributes will be pruned. 

### Using the `relevant` facet of `fx-bind`

Besides simple existence of a data item the `fx-bind` element may specify a `relevant` condition for a data item of a set of items.

The expression needs to evaluate to a Boolean and will be taken into account when refreshing the UI or sending data.

Example:
```
<fx-fore>
  <fx-model>
    <fx-instance>
      <data>
        <vehicle type="bicycle">
        <bicycle>
          <frame size="28"></frame>
        <bicycle>
        <car>
          <engine>
        </car>
      </data>
    </fx-instance>
    <fx-bind ref="bicycle" relevant="../vehicle/@type = 'bicycle'></fx-bind>
    <fx-bind ref="car" relevant="../vehicle/@type = 'car'></fx-bind>
  </fx-model>
</fx-fore>
```

When sending data these bindings will make sure that only the relevant portions of the data are sent by default, depending on the value of `vehicle/@type`.

Likewise when a user makes a selection for `vehicle/@type' the user interface will adapt and show the relevant controls and hide the nonrelevant ones.


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

 
