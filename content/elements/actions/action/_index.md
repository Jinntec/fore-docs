---
title: "<fx-action>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, actions, action ]
weight: 1
---

### Description

`<fx-action>` is a container action element that can take other actions
as children and defer their update cycle to the end of the action block.

This is useful when you e.g. want to set several values at once without the cost of 
each action to be recalculated, revalidated and refreshed.

### Script Actions

It is possible to call JavaScript from an `<fx-action>` by using the `src` attribute. For an example
see [script actions](../demo/script-actions.html) or the source of this file (doc/reference.html).

### Attributes

| Name | Description |
|------|-------------|
| src | optional attribute to point to a JavaScript file containing a single function to be called. |


### Examples

* <a href="{{% siteparam "demoUrl" %}}actions.html" target="_blank">Actions</a>
* <a href="{{% siteparam "demoUrl" %}}delay.html" target="_blank">the 'delay' attribute</a>
* <a href="{{% siteparam "demoUrl" %}}events.html" target="_blank">Events</a>
* <a href="{{% siteparam "demoUrl" %}}events2.html" target="_blank">Custom Events</a>
* <a href="{{% siteparam "demoUrl" %}}submission1.html" target="_blank">Submission Demo</a>
* <a href="{{% siteparam "demoUrl" %}}submission3.html" target="_blank">Submission Chaining</a>

