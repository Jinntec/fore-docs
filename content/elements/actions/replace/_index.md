---
title: "<fx-replace>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions]
weight: 100
---

### Description

Replaces a node with another, structurally - the target node is entirely swapped out for (a clone of) the replacement node, including its tag name, attributes and children. Use this whenever the *node itself*, not just its string value, needs to be replaced (e.g. round-tripping structured XML from an external editor widget). If you only need to set a string value while keeping the bound node's own identity intact, use [`fx-setvalue`]({{% ref "/elements/actions/setvalue" %}}) instead.

### Attributes

| Name | Description |
|------|-------------|
| ***ref*** | XPath reference pointing to the bound node | - |
| with | XPath expression to point to a node for replacement |


### Examples

* [Replace Action]({{% siteparam "demoUrl" %}}fx-replace.html)



