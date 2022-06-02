---
title: "<fx-model>"
date: 2022-05-20T16:08:59+02:00
tags: [model]
weight: 1
---
## Description

The model is responsible for:
* creating and maintaining the Main Dependency Graph (MDG)
* creating ModelItems for bound data nodes
* calculation 
* validation

The `<fx-model>` element is a direct child of `<fx-fore>` and is itself a container for:
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

## Attributes

none

## Events

| Event | Description | Details
| ------------ | --- | --- |
| model-construct | first event to be emitted by Fore | - |
| model-construct-done | emitted when model has been initialized | - |
| rebuild-done | when a rebuild has taken place | 'maingraph' - the maingraph object being used
| recalculate-done | when a recalculation has taken place | 'subgraph' - the subgraph object being used