---
title: "<fx-refresh>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions, refresh]
weight: 90
---

## Description

Triggers immediate refresh.

## Attributes

| Name | Description                                                    |
|------|----------------------------------------------------------------|
| control | id of an control to be refreshed explicitly                    |
| force | marker attribute to force a full refresh - overrules `control` |
| self | searches upwards for `fx-control` and refreshes it |

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

* [the delay attribute]({{% siteparam "demoUrl" %}}delay.html)
* [Randomizer]({{% siteparam "demoUrl" %}}randomizer.html)
* [the while attribute]({{% siteparam "demoUrl" %}}while.html)



