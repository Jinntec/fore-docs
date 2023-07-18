---
title: "<fx-load>"
date: 2023-01-16T12:00:00+01:00
tags: [elements actions, load]
weight: 70
---

## Description

Loads some content into a page, open a new tab with content or replaces
current browser window with content.

Content may be loaded from `url` or be specified inline surrounded with a `template` element.

## Attributes

| Name      | Description                                  | default |
|-----------|----------------------------------------------|---------|
| attach-to | '_self', '_blank' or idref prefixed with '#' | _self   |
| url       | URL to load content from                     |         |

## Events

| Name       | Description                                 |
|------------|---------------------------------------------|
| url-loaded | dispatched after successful load of content |


## Examples

* [load]({{% siteparam "demoUrl" %}}load.html)



