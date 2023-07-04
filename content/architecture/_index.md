---
title : "Architecture"
date : 2020-12-11T10:42:31+01:00
chapter : true
isHome : true
tags: ["Version 1.0.0", MVC]
---

# Architecture

This chapter gives some insights into the inner workings of Fore.
An understanding of the principles certainly helps to get the most out of Fore.

![MVC](/images/mvc.svg)

Fore is build as a classical MVC architecture.

* **M**odel -> `<fx-model>` Element
* **V**iew -> Fore UI Elements
* **C**ontroller -> Fore Action Elements

## The ForeBody

At the very minimum there needs to be a `fx-fore` element to get Fore into live. Without content this won't do anything
so we can consider these a unit and call it a 'ForeBody'. Adding Fore to your page means to add a ForeBody.

The `fx-fore` element creates a scope for everything contained within it. By default Fore lives in lightDOM and is fully
accessible to global styling. However there are options to put Fore also into shadowDOM if that's necessary or
preferred.


```
<fx-fore>
    <!-- the ForeBody -->
</fx-fore>
```

> Styling-wise the `fx-fore` element is layout-neutral.

### What fx-fore does

The `fx-fore` element is responsible for:
* kick off processing
* initing UI
* refreshing the UI
* messaging

> The detailed initialization process is described under 'Initialization'.

## Fore Model

The Fore model is a container element for data, constraints, requests and custom functions. As Actions can 
occur in all places there might be also a couple of Actions.

```
<fx-fore>
    <fx-model>
        <!-- 1 to n -->
        <fx-action></fx-action>
        
        <!-- 1 to n -->
        <fx-instance></fx-instance>

        <!-- 0 to n -->
        <fx-bind></fx-bind>
        
        <!-- 0 to n -->
        <fx-submission></fx-submission>

        <!-- 0 to n -->
        <fx-function></fx-function>
    </fx-model>
</fx-fore>
```

> the `fx-model` element is a head-less element - it does not display at all and is layout-neutral.

### What the model does

When a model is constructed it will perform some steps to enable efficient processing throughout the lifecycle. 

#### rebuild

During rebuild all `fx-bind` elements are traversed and a DependencyGraph for the data is constructed.

For each bind the `ref` attribute is evaluated with XPath and results in a nodeset of matching data nodes (if any).
For each of those a ModelItem object will be created that wraps the data node and additionally holds it's state.

During the next step the other attributes of bind are examined to detect 'foreign nodes'. Each 'foreign node' will 
become a new dependency in a directed Dependency Graph.

rebuild finishes by dispatch `rebuild-done` event.

#### recalculate

`recalculate` will first check if there have been changes since last run. 

If there are no changes - usually only the case when initializing - the freshly-build mainGraph is used to 
determine the correct calculation order of the graph. The resulting list is iterated and each ModelItem will recompute
its `calculate` expression.

If there have been changes to data nodes these are reported in a 'changed' list. This list is used to build s subgraph
of the mainGraph only containing the affected nodes. These are then computed as above.

#### revalidate

During revalidation the other possbile attributes of `fx-bind` are evaluated using the `ref` expression as context.

These facets result in Boolean values that are assigned to the ModelItem. At refresh time the ModelItem is then
used to synchronize the model state with the UI state and reflecting states like 'readonly' to the HTML attribute.

Evaluating the 'constraint' attribute will add an alert to the ModelItem if defined.

