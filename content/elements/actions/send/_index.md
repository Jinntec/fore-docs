---
title: "<fx-send>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions]
---

### Description

Triggers a submission. Submission with given id must exist otherwise
error is thrown.

### Attributes

| Name | Description | 
|------|-------------| 
| ***submission*** | required idref to `fx-submission` element. |

### Action Attributes

| Name | Description |
|------|-------------|
| delay | delay before action is executed in milliseconds. |
| event | the event name this action is listening to |
| if | boolean XPath expression. Action is only executed if this returns true. |
| target | id reference to element this action attaches to |
| while | boolean XPath expression. Action is only executed if `ìf` and `while` return true. |

## Events

none

### Examples

* [auth]({{% siteparam "demoUrl" %}}auth.html)
* [Submission Relevance Processing]({{% siteparam "demoUrl" %}}submission-relevance.html)
* [Submission serialization]({{% siteparam "demoUrl" %}}submission-serialize.html)
* [Submission Demo]({{% siteparam "demoUrl" %}}submission1.html)
* [Submission Demo 2]({{% siteparam "demoUrl" %}}submission2.html)
* [Submission serialization]({{% siteparam "demoUrl" %}}submission3.html)
* [Submission Chaining]({{% siteparam "demoUrl" %}}submission4.html)
* [submit with ref]({{% siteparam "demoUrl" %}}targetref.html)



