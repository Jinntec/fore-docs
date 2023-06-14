---
title: "<fx-send>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions]
weight: 130
---

### Description

Triggers a submission. Submission with given id must exist otherwise
error is thrown.

### Attributes

| Name | Description                                                                                       | 
|------|---------------------------------------------------------------------------------------------------| 
| ***submission*** | required idref to `fx-submission` element. Also supports '#reload' which just reloads the window. |
| target | overwrites target attribute of submission - may contain template expressions |
| url | overwrites url attribute of submission - may contain template expressions |

> Attributes that overwrite submission attributes are set once per execution. Calling the same submission again without such an attribute falls back to the value on `fx-submission` element.  
  
## Events

| Name | Description                                                                                       | 
|------|---------------------------------------------------------------------------------------------------| 
| log | log event is dispatched in case submission id cannot be found |

### Examples

* [auth]({{% siteparam "demoUrl" %}}auth.html)
* [Submission Relevance Processing]({{% siteparam "demoUrl" %}}submission-relevance.html)
* [Submission serialization]({{% siteparam "demoUrl" %}}submission-serialize.html)
* [Submission Demo]({{% siteparam "demoUrl" %}}submission1.html)
* [Submission Demo 2]({{% siteparam "demoUrl" %}}submission2.html)
* [Submission serialization]({{% siteparam "demoUrl" %}}submission3.html)
* [Submission Chaining]({{% siteparam "demoUrl" %}}submission4.html)
* [submit with ref]({{% siteparam "demoUrl" %}}targetref.html)
* [overwrite url]({{% siteparam "demoUrl" %}}submission-url-overwrite.html)
* [overwrite url]({{% siteparam "demoUrl" %}}submission-target-overwrite.html)



