---
title: "Lifecycle"
menuTitle: ""
date: 2025-02-13T11:42:44+01:00
tags: []
---

* model-construct
* rebuild
* recalculate
* revalidate
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


    
        Note over Model: rebuild phase
        Model->>Model: rebuild()
        loop: fx-bind 
        Model->>FxBind: init()

        FxBind->>NodeBinding:create NodeBinding for ref
        NodeBinding->>NodeBinding:constructor
        NodeBinding-->>DependencyTracker:register(xpath:node,NodeBinding)

        activate NodeBinding
        loop: facets
            NodeBinding->>FacetBinding:create FacetBinding for facet
            FacetBinding-->>DependencyTracker:register(FacetBinding)
        end
    deactivate NodeBinding
        
        loop: forEach dependency in facet xpath
        activate FacetBinding
            FacetBinding->>NodeBinding:create NodeBinding for dep
            NodeBinding-->>DependencyTracker:register(xpath:node,NodeBinding)

            FacetBinding-->>DependencyTracker: registerDependency(nodeXPath,facetXPath)
        end
        deactivate FacetBinding

            
    end
    
    
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
            DependencyTracker->>DependencyTracker: add pending Binding to subgraph

            loop: dependencies
                DependencyTracker->>DependencyTracker: add depencency to subgraph
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
