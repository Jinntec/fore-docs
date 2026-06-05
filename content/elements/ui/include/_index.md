---
title: "<fx-include>"
menuTitle: ""
tags: [elements, ui, fx-include]
weight: 24   
---
## Description

`<fx-include>` lazily loads markup from a local template or external HTML source into its own light DOM immediately or when a configured event occurs.

Inclusion can be immediate or be triggered by an event. It can be 'one-time' or reloadable. Either inline templates and external sources are supported.

Motivations to use `<fx-include>` are:

* splitting large pages into pieces for ease of authoring and modular organisation
* reducing runtime load with large pages by loading on demand 

## Attributes

| Name      | Description                                                                       | Default |
|-----------|-----------------------------------------------------------------------------------|---|
| event | the event to listen for to trigger inclusion | click |
| immediate | when attribute is present the content will be loaded immediately at load time     | false |
| reload | when attribute is present inclusion will be retriggered by each event occurrences | false |
| replace | replaces the `fx-include` itself with the loaded content - reload will not apply any more | false |
| selector | optional CSS selector to apply to included source | - | 
| src | external html source to be included - if not given a template element must exist  | - |
| target | the target element to listen on for configured event | - |

## Events

| Name         | Description                           |
|--------------|---------------------------------------|
| include-done | dispatched when inclusion has happend |
| error | when no source is given, the loading failed or selector couldn't be applied |

## Examples





