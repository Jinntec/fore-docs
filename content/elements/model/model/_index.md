---
title: "<fx-model>"
date: 2022-05-20T16:08:59+02:00
tags: [model]
weight: 1
---

The model is a direct child of `<fx-fore>` and is itself a container for:
* one or more `<fx-instance>` elements
* zero, one or more `<fx-bind>` elements
* zero, one or more `<fx-submission>` elements
* zero, one or more `<fx-function>` elements

```
<fx-model>
    <fx-instance><fx-instance>
    <fx-instance id="second"><fx-instance>
    <fx-instance id="third"><fx-instance>
    
    <fx-bind></fx-bind>
    <fx-bind></fx-bind>
    ...
    
    <fx-submission id="load"></fx-submission>
    <fx-submission id="save"></fx-submission>
</fx-model>
```

If there's more than one `<fx-instance>` or `<fx-submission>` you need
to add an `id` attribute for identification.

