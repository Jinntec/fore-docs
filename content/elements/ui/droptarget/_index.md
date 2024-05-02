---
title: "Droptarget"
menuTitle: ""
date: 2024-05-02T13:45:49+02:00
tags: []
---

## Description

`fx-droptarget` only applies when using Drag and Drop is used and acts as 
a sink for HTML draggable elements. `fx-droptarget` can and often will be a draggable element 
itself.

To enable Drag and Drop operation add the `draggable` attribute to the respective elements and add as many
`fx-droptarget` elements as needed. 

Drag and Drop can be used in a lot of different scenarios. The current implementation offers:
* re-ordering bound data in a repeated section (see kanban example)
* moving unbound elements in the UI
* copying unbound elements to a `fx-droptarget`
* constraining what can be dropped onto a droptarget


## Attributes
| Name          | Description                                       | Default |
|---------------|---------------------------------------------------|---|
| accept        | CSS selector matching elements that are accepted  | * |
| drop-action   | one of 'copy' or 'move'                           | move |


## CSS 
| Selector   | Description                                                                              |
|------------|------------------------------------------------------------------------------------------|
| .drag-over | applied whenever a draggable is dragged over the `fx-droptarget`                         |
| .no-drop   | applied whenever a draggable is dragged over the `fx-droptarget` but drop is not allowed |

## Events

none

## Examples

* [Drag and Drop]({{% siteparam "demoUrl" %}}drag-drop-interface.html)
* [Kanban Board]({{% siteparam "demoUrl" %}}kanban.html)
