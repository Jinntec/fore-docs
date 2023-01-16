---
title: "<fx-load>"
date: 2023-01-16T12:00:00+01:00
tags: [elements actions, load]
---

## Description

Loads some content into a page, open a new tab with content or replaces
current browser window with content.

## Attributes

| Name      | Description                                  | default |
|-----------|----------------------------------------------|---------|
| attach-to | '_self', '_blank' or idref prefixed with '#' | _self   |
| url       | URL to load content from                     |         |

## Action Attributes

| Name | Description |
|------|-------------|
| delay | delay before action is executed in milliseconds. |
| event | the event name this action is listening to |
| if | boolean XPath expression. Action is only executed if this returns true. |
| target | id reference to element this action attaches to |
| while | boolean XPath expression. Action is only executed if `ìf` and `while` return true. |

## Events

| Name       | Description                                 |
|------------|---------------------------------------------|
| url-loaded | dispatched after successful load of content |


## Examples

* [load]({{% siteparam "demoUrl" %}}load.html)



