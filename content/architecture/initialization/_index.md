---
title: "Initialization"
date: 2021-12-14T17:41:11+01:00
tags: [architecture, lifecycle, initialization]
---

A defined lifecycle is essential for consistent and efficient processing of state changes during the lifetime
of a `<fx-fore>` element. 

The diagram below might read a bit complex at first sight but pretty much touches all important areas of Fore
and might be a useful read for the interested developer.

## Initialization of Fore

{{<mermaid align="left">}}
sequenceDiagram
    autonumber
    participant Fore
    participant Model
    participant Instances
    participant Bindings
    participant UI
    Note over Fore: find or generate Model
    activate Model
    Fore->>Model: modelConstruct()
    
    loop
        Model->>Instances: init()
    end
    Instances-->>Model: instance-loaded
    
    activate Model
    Model->>Model: rebuild()
    loop
        Model->>Bindings: init()
        activate Bindings
            Bindings->>Model: ModelItems
        deactivate Bindings
    end
    deactivate Model
    
    Model->>Model: recalculate()
    
    Model->>Model: revalidate()

    Model-->>Fore: modelConstructDone
    activate Fore
    Fore->>Fore: initUI()
    loop
        Fore->>UI: refresh()
        activate UI
            UI->>UI: updateState
        deactivate UI
    end
    Fore-->>Fore: refresh-done
    Fore-->>Fore: ready
    deactivate Fore
    deactivate Model

{{< /mermaid >}}

1. When a `<fx-fore>` element gets connected, it will wait for all children to be connected and then call `modelConstruct()`
on the `<fx-model>` element to kick off the initialization process. If no `<fx-model>` is present one will be created. A `model-construct`
event will be emitted.
1. The model will look for all `<fx-instance>` elements within its child elements and call `init()` for each of them. This 
might involve loading data from an URL. 
1. A `instance-loaded` event will be dispatched for each instance once it's loaded.
1. During `rebuild()` the model will build its dependency graph by inspecting all `<fx-bind>` elements within the model.
1. For each data node a `ref` attribute is pointing to a `ModelItem` object is created that holds the state of the 
data node. By inspecting the `calculate`, `constraint`, `readonly`, `relevant` and `required` attributes of a Bind the dependencies between
data nodes are detected and added to the Main Dependency Graph (MDG).
1. ModelItems will be registered in a map object in the Model. The data node itself will be the key to the ModelItem state object.
1. `recalculate()` evaluates all `calculate` attributes in the order given by the MDG.
1. `revalidate()` evaluates all `constraint`, `readonly`, `relevant` and `required` attributes to determine the validity of a ModelItem.
1. `model-construct-done` event is emitted and catched by `<fx-fore>` element.
1. Fore executes `initUI` which will find all bound elements within the scope of the `<fx-fore>` element.
1. Call `refresh()` for each of them. 
1. Synchronize UI element state with ModelItem state by evaluating binding expression, fetching ModelItem object from Model
and applying the relevant changes to a control.
1. Fore dispatches a `refresh-done` event once all UI elements have been refreshed
1. Fore dispatches a 'ready' event


