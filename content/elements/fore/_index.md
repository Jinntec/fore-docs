---
title: "fx-fore"
date: 2022-05-20T16:08:59+02:00
tags: [fore]
weight: 1
---

The `<fx-fore>` element establishes a scope of processing similar
to a HTML `<form>` element. It is a container for all other Fore elements
and provide the following facilities:

* inits a Fore session
* refreshes the UI
* global messaging with toast or modal messages

## Attributes

| Name | Description | default |
|------|-------------|------- |
| src | url to load a `<fx-fore>` element from another HTML file | - |

## Events

| Name | Description |
|------|-------------|
| compute-exception | dispatched in case the dependency graph is cirular |
| refresh-done | dispatched after a refresh() run |
| ready | dispatched after Fore has fully been initialized |
| error | dispatches error when template expression fails to evaluate |


## Examples

All <a href="{{% siteparam "demoUrl" %}}" target="_blank">Demo</a> files

