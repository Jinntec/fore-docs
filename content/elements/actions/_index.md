---
title: "Actions"
menuTitle: "Action Elements"
date: 2021-12-14T17:41:11+01:00
weight: 180
tags: [elements actions]
chapter: true
---

# Action Elements

This chapter describes all Action elements.

![Fore Actions](/images/actions.svg)

{{% notice note %}}
Action elements have no visual representation and are always hidden
from view.
{{% /notice %}}

## Common Attributes

The following attribues can be used on any Fore action element.

| Name          | Description                                                                        |
|---------------|------------------------------------------------------------------------------------|
| defaultAction | 'perform' (default) or 'cancel'                                                    |
| delay         | delay before action is executed in milliseconds.                                   |
| event         | the event name this action is listening to                                         |
| if            | boolean XPath expression. Action is only executed if this returns true.            |
| phase         | 'default' or 'capture'                                                             |
| propagate     | 'stop' or 'continue' (default)                                                     |
| target        | id of element to attach to or special values '#window' and '#document'  |
| while         | boolean XPath expression. Action is only executed if `ìf` and `while` return true. |


## Common Events

| Name             | Description                                |
|------------------|--------------------------------------------|
| action-performed | dispatched after execution of an action    |
| while-performed  | dispatched after execution of a while loop |



