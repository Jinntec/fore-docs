---
title: "Events"
date: 2021-12-14T17:41:11+01:00
weight: 3
chapter: true
tags: [events]
---

# Events

Fore is an event-driven state-engine. It reacts to events and dispatches itself events to reflect it's state. Each operation in Fore is triggered by some event. You can hook your
functionality into the page by defining actions for a given event.


## Lifecycle Events

Lifecylce events can be used for initialization tasks. When Fore is loaded into the DOM of a web page it will
dispatch the following sequence of events:

| Name | Description | target     |
|------|-------------|------------| 
| `model-construct` | is not of much practical use but just signals that Fore is alive | `fx-model` |
| `model-construct-done` | fires after all `fx-instance` elements have initialized and the model is setup. At this point we can rely on the existence of the referenced data. | `fx-model` |
| `rebuild-done` | is emitted when the model was rebuild. During this stage Fore creates its dependency graph. | `fx-model`  |
| `recalculate-done` | is emitted when the model was recalculated. During this stage Fore evaluates the dependency graph. | `fx-model`  |
| `refresh-done` | is emitted when the UI has been updated fully. Data in the model are now reflected in the UI. | `fx-fore`  |
| `ready` | is dispatched when the current Fore element is fully initialized and rendered | `fx-fore`|

> For all work that should be done ***before*** the first rendering takes place use a 'model-construct-done' handler. This is the best place to load additional data and do more complex initialization tasks as all actions triggered by 'model-construct-done' will run within a single update cycle.

> On 'ready' you can rely on the UI being fully rendered. This also means that all 'init' events attached to controls have been executed and eventual custom initialization tasks have been run.

## General Events 

A Fore Action can listen to any event. These might the native ones or custom events.

> If events specify a `details` object this can be accessed with the Fore `event('propname')` function. See under Functions.

| Name                 | Description                                           | Target |
|----------------------|-------------------------------------------------------|--------|
| `click`              | just listed here as it might be of frequent interest. | parentNode by default |
| any native JS event | -                                                    | parentNode by default   |
| any custom event | -                                                    | parentNode by default   |

## Update Cycle Events

Some actions mutate data and report this to the model by setting a 'needsUpdate' flag. When an action block is done
it will check for the flag and update the model and UI accordingly by:

* optionally fully rebuild the model constraints (usually avoided)
* recalculate changed items
* revalidate changed items
* refresh controls/containers bound to changed items

| Name              | Description                                                           | Target     | details                                    |
|-------------------|-----------------------------------------------------------------------|------------|--------------------------------------------|
| `rebuild-done`    | fires after a rebuild has taken place                                 | `fx-model` | `maingraph` - the main dependency graph    |
| `recalculate-done` | fires after a recalculate has taken place                             | `fx-model` | `graph` - the depencency main- or subgraph, `computes` - the amount of computes | 
| `refresh-done`    | fires after a refresh has been done. The UI reflects the model state. | `fx-fore`  | -                                          |

## Control State Events

State events are dispatched whenever the state of a bound element changes.

| Name            | Description                                  | Target | Details |
|-----------------|----------------------------------------------|--------|-----|
| `init`          | fires when a control initializes             | `fx-control` | - |
| `readonly`      | fires after an fx-control became readonly    | `fx-control` | - |
| `readwrite`     | fires after an fx-control became readwrite   | `fx-control` | - |
| `optional`      | fires after an fx-control became optional    | `fx-control` | - |
| `required`      | fires after an fx-control became required    | `fx-control` | - |
| `nonrelevant`   | fires after an fx-control became nonrelevant | `fx-control` | - |
| `relevant`      | fires after a fx-control has become relevant | `fx-control` | - |
| `invalid`       | fires after a fx-control has become invalid  | `fx-control` | - |
| `valid`         | fires after a fx-control has become valid    | `fx-control` | - |
| `value-changed` | fires after a fx-control has changed its value  | `fx-control` | `path`- the normalized path of the bound node, `value` - the value of the bound node |

## Instance Events

| Name              | Description                                      | Target                            |
|-------------------|--------------------------------------------------|-----------------------------------|
| `deleted`         | fires after a delete action has been executed    | `fx-instance` |
| `insert`          | fires when an fx-insert is executed    | `fx-instance` |
| `instance-loaded` | fires after an fx-instance has been loaded    | `fx-instance` |

## Submission Events
| Name           | Description                                | Target         | Details                                     |
|----------------|--------------------------------------------|----------------|---------------------------------------------|
| `submit`       | dispatch before submission is taking place | `fx-submission` | `submission` - the `fx-submission` element |
| `submit-done`  | fires after a submission has successfully been executed | `fx-submission` | -                                           |
| `submit-error` | fires when a submission returned an error | `fx-submission` | `message` - the submit error                |


## Repeat Events
| Name                | Description                                    | Target      |
|---------------------|------------------------------------------------|-------------|
| `item-created`      | fires when a repeat item was created           | `fx-repeat` | `nodeset`- the repeatitem nodeset, `pos`- the index position |
| `item-changed`      | fires when a repeat item was changed           | `fx-repeat` | `nodeset' - the nodeset, `pos`- the new index |
| `path-mutated`      | fires when a path in a repeat has been mutated | `fx-repeat` | `path` - the normalized path of the mutation |
| `no-template-error` | fires when repeat has no template child        | `fx-repeat` | `message` - the error message |



## Switch events
| Name          | Description                            | Target                                      |
|---------------|----------------------------------------|----------------------------|
| `deselect` | fires when fx-case is deselected | `fx-case` element that was deselected |
| `select` | fires when fx-case is deselected | `fx-case` element that was selected |

## Dialog Events

| Name          | Description                            | Target                                      |
|---------------|----------------------------------------|----------------------------|
| `dialog-hidden` | fires after fx-dialog has been hidden | `fx-dialog` |
| `dialog-shown` | fired when a dialog has been shown | `fx-dialog`|

## Other
| Name                     | Description                                                    | Target             | Details                                                                                           |
|--------------------------|----------------------------------------------------------------|--------------------|---------------------------------------------------------------------------------------------------|
| `error`                  | fires after an error occurred                                  | `fx-fore`          | `message` - the error message                                                                     |
| `execute-action`         | fires when an action executes. For internal use.               | any action element | `action' - the action element, `event`- the event object                                          |
| `loaded`                 | fires after a fx-load has loaded or a sub-Fore has been loaded | `fx-load`          | `url` - the evaluated url used by the load action, `fore` - the Fore element that has been loaded |
| `outermost-action-start` | fires when an outermost action block is started                | `fx-action`        | `cause` - the event object causing the action                                                     |
| `outermost-action-end`   | fires when an outermost action block is finished               | `fx-action`        | -                                                                                                 |                                                       |
| `reload`                 | fires when a fx-reload action executes                         | `fx-reload`      | -                                                                                                 |
| `return`                 | fired by embedded Fore controls to return their bound value    | `fx-fore`          | `nodeset` - the nodeset returned by a subpage                                                     |
| `warn`                   | dispatched internally by Fore to display warning messages      | `fx-fore`          | `message` - the warning message                                                                   |                         |


