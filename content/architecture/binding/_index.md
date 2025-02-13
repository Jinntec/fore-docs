---
title: "Binding"
menuTitle: ""
date: 2025-01-30T11:24:48+01:00
tags: []
---

UI Binding

{{<mermaid align="left">}}
sequenceDiagram
autonumber
participant Fore
participant boundElement

    Note over Fore: initUI()
    Fore->>Fore: refresh(force=true)
    loop
        Note right of Fore: binding data and control
        Fore->>boundElement: refresh(force=true)
    end
{{< /mermaid >}}
