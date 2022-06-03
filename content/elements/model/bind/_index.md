---
title: "<fx-bind>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, model, fx-bind]
---

## Description

`fx-bind` element attaches constraints and calculations to instance nodes.

## Attributes

| Name | Description | Default |
|------|-------------| --- |
|ref | XPath pointing to node(s) the bind is attaching to | - |
| calculate | XPath expression to be calculated. Result will become value of node(s) referenced by `ref` | - |
| constraint | boolean XPath expression to determine validity of node(s) | true |
| readonly | boolean XPath expression to determine readonly/readwrite state | false |
| relevant | boolean XPath expression to determine relevant/non-relevant state | true |
| required | boolean XPath expression to determine required/optional state | false |
| type | datatype - reserved for future versions | string |

## Events

none

## Examples

* [nested Binding]({{% siteparam "demoUrl" %}}binding-nested.html)
* [Binding]({{% siteparam "demoUrl" %}}binding.html)
* [Hello]({{% siteparam "demoUrl" %}}body.html)
* [Simple Calculate]({{% siteparam "demoUrl" %}}calc-order.html)
* [todo]({{% siteparam "demoUrl" %}}nested-todo.html)
* [Recalculate]({{% siteparam "demoUrl" %}}recalculate.html)
* [Revalidation]({{% siteparam "demoUrl" %}}revalidate.html)
* [Submission Relevance Processing]({{% siteparam "demoUrl" %}}submission-relevance.html)

