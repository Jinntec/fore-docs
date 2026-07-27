---
title: "<fx-container>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui]
weight: 10
---

`<fx-container>` is an abstract class used for container controls 
like `<fx-group>` and `<fx-switch>`.

## Attributes

| Name | Description                                                                                                                    | Default |
|------|--------------------------------------------------------------------------------------------------------------------------------|---------|
| readonly | boolean attribute - if present, marks the container (and its contents) readonly. Usually calculated via bind.                  | false |
| refresh-on-view | when used together with `src`, (re-)loads the referenced content each time the container becomes visible, instead of only once | false |
| src | url to lazily load content from                                                                                                | - |


