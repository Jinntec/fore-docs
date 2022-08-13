---
title: "<fx-setfocus>"
date: 2022-08-12T12:00:00+01:00
tags: [elements actions]
weight: 110
---

### Description

Sets the focus to a control with given id. If the id
is within an repeat it will look for the active repeatitem
and search that for the control. 

### Attributes

| Name    | Description                         |
|---------|-------------------------------------|
| control | idref that a control                |


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

* [todo]({{% siteparam "demoUrl" %}}todo2.html)


