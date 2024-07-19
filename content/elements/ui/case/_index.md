---
title: "<fx-case>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui, fx-case, fx-switch]
weight: 5
---

## Description

Defines one 'page' of a `fx-switch` element.

## Attributes

| Name | Description                                                  |
|------|--------------------------------------------------------------|
| label | optional label                                               |
| name | a unique name to be used with `fx-toggle`                    |
| selector | a CSS selector to select a certain element from external src |
| src | a URL being used for fetching the content of a case          | 


## Events

| Name | Description |
|------|-------------|
| select | dispatched to `fx-case` when a case gets selected |
| deselect | dispatched to `fx-case` when case gets deselected |
  
## Examples

* [Repeat in Switch]({{% siteparam "demoUrl" %}}repeat-in-switch.html)
* [TEI header editor sample]({{% siteparam "demoUrl" %}}simple-tei-header.html)
* [Switch]({{% siteparam "demoUrl" %}}switch.html)



