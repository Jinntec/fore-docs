---
title: "fx-fore"
date: 2022-05-20T16:08:59+02:00
tags: [fore, fx-fore, v1.6.x]
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
| src | url to load a `<fx-fore>` element from another HTML file                 | -       |
| show-confirmation | either just marker attribute or boolean XPath |  -      |
| [foreign attributes] | Foreign attributes are all other attributes being present. These will be copied to the resulting `fx-fore` element if `src` is used for loading an external page. These can be accessed with the `fore-attr()` function | - | 

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



## Examples

* All <a href="{{% siteparam "demoUrl" %}}" target="_blank">Demo</a> files
* [page exit confirmation]({{% siteparam "demoUrl" %}}beforeunload.html)
