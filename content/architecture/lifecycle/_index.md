---
title: "Lifecycle"
menuTitle: ""
date: 2025-02-13T11:42:44+01:00
tags: [ ]
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
    
    activate FxBind
        loop: this.nodeset
            FxBind->>NodeBinding:new NodeBinding(modelIitem,fore)
            activate NodeBinding
                NodeBinding-->>DependencyTracker:registerBinding(xpath:node,NodeBinding)
                NodeBinding-->>DependencyTracker:registerDependencies(xpath:node,NodeBinding)
            
                activate NodeBinding
                    NodeBinding->>NodeBinding: registerFacets()
                    NodeBinding->>FacetBinding:new FacetBinding(modelItem, 'calculate')
                    NodeBinding-->>DependencyTracker:registerBinding(FacetBinding)
                    NodeBinding-->>DependencyTracker:registerDependency(xpath, xpath:calculate)
            
                    NodeBinding->>FacetBinding:new FacetBinding(modelItem, 'constraint')
                    NodeBinding-->>DependencyTracker:registerBinding(FacetBinding)
                    NodeBinding-->>DependencyTracker:registerDependency(xpath, xpath:constraint)
            
                    NodeBinding->>FacetBinding:new FacetBinding(modelItem, 'readonly')
                    NodeBinding-->>DependencyTracker:registerBinding(FacetBinding)
                    NodeBinding-->>DependencyTracker:registerDependency(xpath, xpath:readonly)
                    NodeBinding->>NodeBinding:_addFacetDependencies()
        
                    NodeBinding->>FacetBinding:new FacetBinding(modelItem, 'relevant')
                    NodeBinding-->>DependencyTracker:registerBinding(FacetBinding)
                    NodeBinding-->>DependencyTracker:registerDependency(xpath, xpath:relevant)
                    NodeBinding->>NodeBinding:_addFacetDependencies()
        
                    NodeBinding->>FacetBinding:new FacetBinding(modelItem, 'required')
                    NodeBinding-->>DependencyTracker:registerBinding(FacetBinding)
                    NodeBinding-->>DependencyTracker:registerDependency(xpath, xpath:required)
                    NodeBinding->>NodeBinding:_addFacetDependencies()
        
                    loop
                        NodeBinding->>DependencyTracker: mainGraph.addNode(xpath,node)
                        NodeBinding->>DependencyTracker: mainGraph.mainGraph.addDependency(facetKey, xpath)
                    end
            deactivate NodeBinding
        end
    deactivate FxBind
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
                Binding->>DependencyTracker: pendingUpdates.delete(this)
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

## Refresh
{{<mermaid align="left">}}
sequenceDiagram

title: refresh()
autonumber
participant Fore
participant BoundElement
participant Model
participant UIBinding
participant DependencyTracker

activate Fore
    Note over Fore: first refresh after page load
    Fore ->> Fore: refresh()
    loop: iterate bound children
        Fore->>BoundElement: refresh()
        activate BoundElement
            BoundElement->>Model: getModelItem()
            BoundElement->>UIBinding: new()
            BoundElement->>DependencyTracker: registerBinding(UIBinding)
            BoundElement->>BoundElement: updateWidgetValue()
            BoundElement->>BoundElement: handleModelItemProperties()
        deactivate BoundElement
    end
    Fore->>Fore: dispatch 'refresh-done'

deactivate Fore
activate Fore
    Note over Fore: subsequent refreshes
    Fore ->> Fore: refresh()

    Fore->>DependencyTracker: if(hasUpdates) processUpdates()
    activate DependencyTracker
        Note right of DependencyTracker: update template expressions of $default scope
        DependencyTracker->>DependencyTracker: update(templateExpression)
        loop: loop all template and control bindings
            Note left of DependencyTracker: Control- or TemplateBinding
            DependencyTracker->>UIBinding: update()
        end
    deactivate DependencyTracker
    DependencyTracker->>Fore:  
    Fore->>Fore: dispatch 'refresh-done'


    
    
    
deactivate Fore

{{< /mermaid >}}


