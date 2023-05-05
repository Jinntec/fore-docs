---
title: "<fx-bind>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, model, fx-bind]
---

## Description

The `fx-bind` element attaches constraints and calculations to instance nodes.
  
 By using XPath expressions for the attributes users can build complex calculation and validation rules (business logic) using a declarative syntax.
  
 `fx-bind`elements can be nested thereby taking part in scope resolution resolving their `ref` attributes relative to their parent element.

The bindings are used to build the MDG (Main Dependency Graph) which detects dependencies between nodes and builds a graph that connects the dependent nodes to the currently processed one. This directed graph will then be ordered for computation. Circular dependencies are not allowed.
  
When nodes are changed by user interaction only affected nodes are recomputed - affected nodes are nodes that have a connection to the changed node in the graph. 

This change detection mechanism also drives efficient updating of the UI by selectively updating only controls that are bound to affected nodes.
  
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

