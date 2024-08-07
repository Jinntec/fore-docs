---
title: "<fx-repeat>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui, fx-repeat, repeat]
weight: 45
---

## Description

Repeats template for each node of the referenced nodeset.

For each data node in the referenced nodeset one `<fx-repeatitem>` element
will be created that will contain the evaluated template as content.


## Attributes

| Name | Description | 
|------|-------------| 
| id | identifier for repeat |
| ***ref*** | XPath reference pointing to the bound node | - |

## Events

| Name | Description | Details
|------|-------------|--- |
| item-created | dispatched when a new repeat entry is created | 'path' - a canonical xpath <br> 'index' - the index of the new item |
| path-mutated | dispatched when repeat nodeset changes | 'path' - the mutation path <br> 'index' - the index of the changed repeat item.
| no-template-error | dispatched when there's no template defined | 'id' - the repeat id |


## Examples

* [API Demo]({{% siteparam "demoUrl" %}}api.html)
* [docbook Bibliography]({{% siteparam "demoUrl" %}}docbook-bibliography.html)
* [insert]({{% siteparam "demoUrl" %}}insert.html)
* [todo]({{% siteparam "demoUrl" %}}nested-todo.html)
* [Project Task planner]({{% siteparam "demoUrl" %}}project.html)
* [Atomic repeat]({{% siteparam "demoUrl" %}}repeat-atomic.html)
* [repeat in switch]({{% siteparam "demoUrl" %}}repeat-in-switch.html)
* [repeat sequence]({{% siteparam "demoUrl" %}}repeat-sequence.html)
* [the while attribute]({{% siteparam "demoUrl" %}}while.html)



