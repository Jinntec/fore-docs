---
title: "Lifecycle"
menuTitle: ""
date: 2025-02-13T11:42:44+01:00
tags: []
---

* model-construct
* rebuild
* recalculate
* model-construct-done
* init-done
* refresh-done
* ready

# Update Cycle

When data mutations happen by Control changes:
* recalculate
* revalidate
* refresh

When data mutations happen by actions (trigger)
* recalculate
* revalidate
* refresh

## Rebuild

{{<mermaid align="left">}}
sequenceDiagram
title:Dependency Tracking
autonumber
participant Model
participant FxBind
participant DependencyTracker
participant NodeBinding
participant FacetBinding


    activate Model
    
        Note over Model: rebuild phase
        Model->>Model: rebuild()
        loop: fx-bind 
        activate FxBind
        Model->>FxBind: init()

        FxBind->>NodeBinding:create NodeBinding for ref
        activate NodeBinding
        NodeBinding->>NodeBinding:constructor
        NodeBinding->>DependencyTracker:register(xpath:node,NodeBinding)
        deactivate NodeBinding

        loop: facets
            FxBind->>FacetBinding:create FacetBinding for facet
            activate FacetBinding

                FacetBinding->>DependencyTracker:register(FacetBinding)
            
            deactivate FacetBinding

            
        end
        
        loop: forEach dependency in facet xpath
            FxBind->>NodeBinding:create NodeBinding for dep
            activate NodeBinding
                NodeBinding->>DependencyTracker: register(xpath,NodeBinding)
            deactivate NodeBinding
        end
        deactivate FxBind
            
    end
    
    
    deactivate Model
{{< /mermaid >}}

## Recalculate

{{<mermaid align="left">}}
sequenceDiagram

title: recalculate()
autonumber
participant Model
participant DependencyTracker

    participant Binding

    
        Note over Model: recalculate phase - first run
        
        
        activate Model
            Model->>DependencyTracker: dependencyGraph
            loop: dependencyGraph.overallOrder()
                Model->>Binding: update()
            end
        


        Note over Model: recalculate with changes
        deactivate Model
        Model->>DependencyTracker: buildSubgraphForChanges

        activate DependencyTracker
        loop
            DependencyTracker->>DependencyTracker: add to subgraph

            loop: dependencies
                DependencyTracker->>DependencyTracker: add to subgraph
            end
        end

        DependencyTracker->>Model: ordered list of changes
        deactivate DependencyTracker

        activate Model

        loop: list
            Model->>Binding: update()
        end
        deactivate Model



{{< /mermaid >}}
