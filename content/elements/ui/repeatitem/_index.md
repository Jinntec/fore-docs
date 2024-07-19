---
title: "<fx-repeatitem>"
menuTitle: ""
date: 2024-07-19T09:31:39+02:00
tags: [UI]
weight: 46
---

## Description

> `fx-repeatitem` is auto-created by `fx-repeat` and MUST NOT be used by page authors directly.

When a `fx-repeat` is initialized it creates a `fx-repeatitem` for each bound node in the repeat nodeset using the repeat.
The repeat template is instanciated once for the bound repeated node and stamped out as a `fx-repeatitem`.

This element acts as a wrapper for repeated items and can receive the boolean attribute `repeat-index` when it
is the currently selected item. By default after initialization the repeat index is always 1.


## Attributes

| Name         | Description                                                                        | 
|--------------|------------------------------------------------------------------------------------| 
| repeat-index | boolean attribute being present when the repeatitem is the currently selected one. |

## Events

| Name         | Description                                           | Details
|--------------|-------------------------------------------------------|--- |
| index-change | dispatched when a repeatitem is clicked or gets focus | 'item' - the repeatitem as node <br> 'index' - the index of the changed repeat item.


## Examples

See [repeat examples](https://jinntec.github.io/fore-docs/elements/ui/repeat/#examples)


