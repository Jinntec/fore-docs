---
title: "<fx-message>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions, message]
weight: 70
---

## Description

Display a message to the user.

## Attributes

| Name | Description | default |
|------|-------------| ------ |
| level | 'modal', 'modeless' or 'ephemeral' | ephemeral |
| | 'modal' - modal dialog window | |
| | 'sticky' - sticky popup message  | |
| | 'ephemeral' - auto-closing popup message  | default |
| value | XPath expression which resolves to message | |

## Action Attributes

| Name | Description |
|------|-------------|
| delay | delay before action is executed in milliseconds. |
| event | the event name this action is listening to |
| if | boolean XPath expression. Action is only executed if this returns true. |
| target | id reference to element this action attaches to |
| while | boolean XPath expression. Action is only executed if `ìf` and `while` return true. |

## Events

none

## Examples

* [fx-message]({{% siteparam "demoUrl" %}}fx-message.html)
* [actions]({{% siteparam "demoUrl" %}}actions.html)
* [Binding]({{% siteparam "demoUrl" %}}binding.html)
* [the delay attribute]({{% siteparam "demoUrl" %}}delay.html)
* [fx-control]({{% siteparam "demoUrl" %}}fx-control.html)
* [Hello World]({{% siteparam "demoUrl" %}}hello-fonto.html)
* [the if attribute]({{% siteparam "demoUrl" %}}if.html)
* [instances]({{% siteparam "demoUrl" %}}instances.html)
* [lazy modelItem creation during UI init]({{% siteparam "demoUrl" %}}lazy.html)
* [the while attribute]({{% siteparam "demoUrl" %}}while.html)



