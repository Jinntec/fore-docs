---
title: "Update Cycle"
date: 2021-12-14T17:41:11+01:00
tags: [architecture, lifecycle, update]
---

The update cycle is triggered whenever a user interacts with a control
e.g. by changing its value.

Likewise this can be triggered by Actions being triggered by some state event like e.g. `value-changed` event.

{{<mermaid align="left">}}
sequenceDiagram
    autonumber
    
    participant User
    participant Control
    participant Action
    participant Model
    participant Fore
    
    User->>Control: interact
    
    Control->>Action: execute
    
    activate Action
        Action->>Action: mutate ModelItem
        Action->>Model: add to changed list
        activate Action
            Action->>Action: actionPerformed()
            Action->>Model: rebuild()
            Action->>Model: recalculate()
            Action->>Fore: changed[] -> toRefresh[]
            Action->>Model: revalidate()
            Action->>Fore: refresh()
            Fore-->>Fore: refresh-done
        deactivate Action
        Action-->>Action: action-performed
    deactivate Action

{{< /mermaid >}}

1. When the value of a UI control changes, it will use an action
to propagate that change to the model.
1. Usually a control will execute a `<fx-setvalue>` action to change
its value
1. The action mutates the ModelItem state object that is associated to the control.
1. The changed ModelItem is added to a `changed` array in the Model
1. When the action has done its job it will call the model to update while executing `actionPerformed()`.
1. Only actions that mutate the structure of the data will call `rebuild()` as the Main Dependency Graph needs
to be reconstructed.
1. Instead of using MDG (see Initialization) `recalculate` will re-compute all calculations for 
the changed nodes by creating a subgraph of the MDG that will only contain the affected ModelItems.
1. The array of changed ModelItems will be cloned and passed as `toRefresh[]` to the Fore object.
1. All ModelItems will be revalidated. 
1. `refresh()` is called on Fore object that will use the `toRefresh` array of changed ModelItems to selectively update
only affected controls. This will also incorporate controls that are dependent on the changed one by using the MDG.
1. A `refresh-done` event is emitted 
1. A `action-performed` event is emitted