---
title: "<fx-delete>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions]
---

## Description

Deletes a node from a nodeset.

## Action Attributes

| Name | Description |
|------|-------------|
| delay | delay before action is executed in milliseconds. |
| event | the event name this action is listening to |
| if | boolean XPath expression. Action is only executed if this returns true. |
| target | id reference to element this action attaches to |
| while | boolean XPath expression. Action is only executed if `ìf` and `while` return true. |

## fx-delete Attributes

| Name | Description |
|------|-------------|
| repeatId | id reference to `fx-repeat` to delete from. If not present `fx-delete` will use next repeatitem in ancestor tree. |


## Examples

* [todo]({{% siteparam "demoUrl" %}}todo.html)
* [nested todo]({{% siteparam "demoUrl" %}}nested-todo.html)
* [TEI header editor sample]({{% siteparam "demoUrl" %}}simple-tei-header.html)




