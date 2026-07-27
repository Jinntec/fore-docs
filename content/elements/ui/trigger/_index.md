---
title: "<fx-trigger>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui, trigger]
weight: 55
---

## Description

Generic container for action buttons, links etc. which can execute 
an action when activated.

`<fx-trigger>` can also be bound and therefore become readonly or non-relevant.

## Attributes

| Name | Description | Default |
|------|-------------| -------- |
| ***ref*** | XPath reference pointing to the bound node | - |
| activate-on-focus | Opt-in: also run the trigger's actions when the slotted element receives focus (e.g. plain Tab-only keyboard navigation), not just on click/Enter/Space. Not the default - every `fx-trigger` in an app would otherwise fire its action (an `fx-delete`, say) just from being tabbed past. A single mouse click still only performs the actions once (click and the focus it causes are deduplicated internally). Useful for "focus follows selection" tree/listbox patterns. | - |

Individual action children can restrict which of the two triggering events they respond to via their own `event` attribute (e.g. `event="click"` on one action while others in the same trigger run for either) - see the action elements' own docs.

## Examples
* [trigger]({{% siteparam "demoUrl" %}}trigger.html)
* [actions]({{% siteparam "demoUrl" %}}actions.html)
* [binding]({{% siteparam "demoUrl" %}}binding.html)
* [delay]({{% siteparam "demoUrl" %}}delay.html)
* [delay]({{% siteparam "demoUrl" %}}delay.html)
* [dispatch]({{% siteparam "demoUrl" %}}fx-dispatch.html)
* [Recursive tree]({{% siteparam "demoUrl" %}}repeat-recursive.html) - `activate-on-focus` for keyboard tree selection
* ...




