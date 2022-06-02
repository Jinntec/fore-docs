---
title: "<fx-control>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui]
---
## Description

`fx-control` is no concrete control displayed in the browser but
instead wraps such a control and binds it to a data node in the model with the help of a `ref` attribute.



## Attributes

| Name | Description | Default |
|------|-------------| -------- |
| context | XPath reference pointing to parent context | incopeContext |
| debounce | optional numeric value in milliseconds to delay input events | - |
| label | optional label | - |
| ***ref*** | XPath reference pointing to the bound node | - |
| updateEvent | optional event name when to trigger updating of bound node. | blur |
| | 'enter' can be used to catch enter key |
| valueProp | optional property name used to set the value of the widget (default:'value') | value |

## Events

| Name | Description |
|------|-------------|
| value-changed | dispatched during refresh after the value of the control has changed |
| optional | dispatched during refresh when node has become optional |
| required | dispatched during refresh when node has become required |
| readonly | dispatched during refresh when node has become readonly |
| readwrite | dispatched during refresh when node has become readwrite |
| valid | dispatched during refresh when node has become valid |
| invalid | dispatched during refresh when node has become invalid |
| relevant | dispatched during refresh when node has become relevant |
| nonrelevant | dispatched during refresh when node has become non-relevant |

## Examples
* [the fx-control element]({{% siteparam "demoUrl" %}}fx-control.html)
* [Actions]({{% siteparam "demoUrl" %}}actions.html)
* [Fore API Demo]({{% siteparam "demoUrl" %}}actions.html)
* [Template Expressions]({{% siteparam "demoUrl" %}}avt.html)
* [Country selector]({{% siteparam "demoUrl" %}}selects.html)
* [Selects]({{% siteparam "demoUrl" %}}selects2.html)
* [Trigger]({{% siteparam "demoUrl" %}}trigger.html)





