---
title: "<fx-fore>"
date: 2022-05-20T16:08:59+02:00
tags: [fore, fx-fore]
weight: 1
---

The `<fx-fore>` element establishes a scope of processing similar
to a HTML `<form>` element. It is a container for all other Fore elements
and provides the following facilities:

* inits a Fore session
* refreshes the UI
* global messaging with toast or modal messages

## Attributes

| Name | Description                                                              | default |
|------|--------------------------------------------------------------------------|---------|
| create-nodes | If attribute is present, non-existing XML data nodes will be created from UI Binding expressions | - |
| ignore-expressions | if given is expected to contain a CSS selector that matches element to excluded from Template Expression handling | - |
| [foreign attributes] | Foreign attributes are all other attributes being present. These will be copied to the resulting `fx-fore` element if `src` is used for loading an external page. These can be accessed with the `fore-attr()` function | - | 
| show-confirmation | either just marker attribute or boolean XPath |  -      |
| src | url to load a `<fx-fore>` element from another HTML file                 | -       |
| strict | boolean attribute - if present error messages will be displayed additionally as toast messages | false |

if `show-confirmation` is just used as a marker attribute Fore will check whether data fields have been modified after initial loading. Attribute may be
empty, the empty string, 'true' or 'show-confirmation'.

Likewise when an XPath expression is given as the attribute value it is evaluated to a boolean to decide wether to show the confirmation.

## Events

| Name              | Description |
|-------------------|-------------|
| compute-exception | dispatched in case the dependency graph is cirular |
| refresh-done      | dispatched after a refresh() run |
| ready             | dispatched after Fore has fully been initialized |
| error             | dispatches error when template expression fails to evaluate |

## create-nodes

The usual behavior for controls is to become 'nonrelevant' and not be shown in the UI if there's no data node matching
the binding expression (`ref`). This allows to show/hide parts of the UI depending on users' choices and is a powerful way to build dynamic UIs.

However this creates problems with other use cases where there's a schema to support and the goal is build an editor for it.

The `create-nodes` attribute solves this common problem with editing XML documents. Quite often a given document does not use all elements and attributes that would be possible from its schema. But to edit the document the UI must show these additional nodes and provide a control to edit them. As there's no node the control can bind to, it has no place to put a value the user inputs. - the node needs to be created first.

Traditional solution to this is to merge the data to be edited with a full template structure containing all possible nodes. However XML merging is not a trivial process when considering all the possible cases. Further it requires extra effort and an additional toolchain to handle this merging and a page author needs to explicitly handle it in a page.

To overcome this issue the `create-nodes` attribute was introduced which will create missing nodes in the data from the UI bindings automatically at startup time. 

Example: assume you have an 'email' field that is not yet present in the edited data. Putting a control into the UI that binds to that field and adding the `create-nodes` attribute to `<fx-fore>` element will create the 'email' node in the right place of the document hierarchy.


```
<fx-fore create-nodes>
  ...
  <fx-control ref="contact/email">
    <label>Email (optional)</label>
  </fx-control>
  ...
</fx-fore>
```

If there would be no other controls the result would be:
```
<data>
  <contact>
    <email>
  </contact>
</data>
```

`create-nodes` will looks for all `ref` expressions in the UI, check if a node already exists and if not, create the necessary nodes from the binding expression. In this case it will first create `contact` and afterwards `email` and attach those to the default instance. 

This happens even before the UI is created and afterwards processsing will continue as usual. Additional `relevant` conditions defined by `<fx-bind ref='something' relevant='some-boolean-expression'>` will apply as expected. 

> XML namespaces are fully supported. To resolve namespaces these must be declared on the `<fx-fore>` element. `<fx-fore xmlns:foo="bar">`.


## Examples

* All <a href="{{% siteparam "demoUrl" %}}" target="_blank">Demo</a> files
* [page exit confirmation]({{% siteparam "demoUrl" %}}beforeunload.html)
* [ignore expressions]({{% siteparam "demoUrl" %}}ignore.html)
