---
title: "<fx-repeat>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui, repeat]
---

## Description

Repeats template for each node of the referenced nodeset.


## Attributes

| Name | Description | 
|------|-------------| 
| id | identifier for repeat |
| ***ref*** | XPath reference pointing to the bound node | - |

## Events

| Name | Description | Details
|------|-------------|--- |
| path-mutated | dispatched when repeat nodeset changes | 'path' - the mutation path <br> 'index' - the index of the changed repeat item.
| refresh-done | dispatched after a refresh() run | - |
| ready | dispatched after Fore has fully been initialized | - |
| error | dispatches error when template expression fails to evaluate | 'message' - the error message |


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



