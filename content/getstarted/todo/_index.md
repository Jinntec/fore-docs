---
title: "todo"
menuTitle: "a more complex example"
date: 2022-05-20T16:08:59+02:00
weight: 3
tags: [basic, repeat, actions, controls]
---

What can be learned here:
* the use of `<fx-repeat>` element
* data binding and resolution
* using a constraint
* using controls
* using insert and delete action

## Todo Application

Let's go for a bit more fancy example and learn about some new elements.

In this tutorial we add some real interaction, give some feedback
messages to the user and actually change our data.

It will introduce you to `<fx-repeat>` element that is one of the container
elements available in Fore.

## Setting up the model

For our todo app we'd like to have a list of todos along with a completion 
and a due date.

Our data model for a single todo looks like this:

```
<task complete="" due=""></task>
```

Lets put that into Fore and add some dummy data to play with.

```
<fx-fore>
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
            </data>
        </fx-instance>
    </fx-model>
</fx-fore>
```

### Introducing `<fx-repeat>`

For displaying a list of todos we'll use the `<fx-repeat>` element
which will show all todos in a list.

We add the repeat alongside the model in our markup.

```
<fx-fore>
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My Todos</h1>
    <fx-repeat id="task" ref="task">
        <template>
            <div>{.}</div>
        </template>
    </fx-repeat>
</fx-fore>
```

### Data Binding - the `ref` Attribute

The `ref` attribute is used throughout Fore on many elements. It uses
**binding expressions** to link to some data node.

In our case the binding expression is simply 'task' and will point to `task` elements
in our data.

```
<fx-fore>
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My Todos</h1>
    <fx-repeat id="task" ref="task">
        <template>
            <div>{.}</div>
        </template>
    </fx-repeat>
</fx-fore>
```

Result so far

<fx-fore>
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My Todos</h1>
    <fx-repeat id="task" ref="task">
        <template>
            <div>{.}</div>
        </template>
    </fx-repeat>
</fx-fore>


A repeat always has a `<template>` child which is the blueprint for rendering
one bound item.

It just contains a div and the Template Expression of '{.}'.

**"."** means the current node which is the bound `task` node.

{{% notice note %}}
This is known as **'scoped resolution'** and means that binding expressions
are always evaluated relatively to their parent binding expression (aka `ref` attributes).
{{% /notice %}}

### Adding controls

In this step we add some controls to the repeat template.

Fore uses a generic `<fx-control>` element to bind a concrete widget (like a native `<input>`) 
to the model.

This has the advantage that there's no need for a big list of different controls
to be supported but instead just use existing ones. 

In this example simple native browser input controls are used.

```
<fx-fore>
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My Todos</h1>
    <fx-repeat id="task" ref="task">
        <template>
            <div>
                <fx-control ref="@complete" value-prop="checked" update-event="input">
                    <input type="checkbox">
                </fx-control>
                <fx-control class="{@complete}" id="task" ref="."></fx-control>
                <fx-control ref="@due">
                    <input type="date">
                </fx-control>
                <fx-trigger class="btn delete">
                    <button>x</button>
                    <fx-delete ref="."></fx-delete>
                </fx-trigger>
            </div>
        </template>
    </fx-repeat>
</fx-fore>
```

{{% notice note %}}
Note the second `<fx-control>` which is empty. If no control
is given as child it will default to a `<input type="text">` control which is
auto-created to save some typing.
{{% /notice %}}

Here 3 `<fx-control>`s  and 2 `<fx-trigger>` elements have been added.

The controls bind to the respective nodes in the data and use:
* a checkbox  for '@complete'
* a text field for task text
* a date input for '@due' date

{{% notice note %}}
The '@' character addresses an attribute of an XML node. Scoped resolution
will result in the binding expression 'task[1]/@complete' for the first todo.
{{% /notice %}}

```
<fx-fore>
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My Todos
        <fx-trigger class="btn add">
            <button>add</button>
            <fx-insert ref="task" at="1" position="before"></fx-insert>
        </fx-trigger>
    </h1>
    <fx-repeat id="task" ref="task">
        <template>
            <div>
                <fx-control ref="@complete" value-prop="checked" update-event="input">
                    <input class="widget" type="checkbox">
                </fx-control>
                <fx-control class="{@complete}" id="task" ref="."></fx-control>
                <fx-control ref="@due">
                    <input type="date">
                </fx-control>
                <fx-trigger class="btn delete">
                    <button>delete</button>
                    <fx-delete ref="."></fx-delete>
                </fx-trigger>
            </div>
        </template>
    </fx-repeat>
</fx-fore>
```

The first `<fx-trigger>` is contained within the `<h1>` and inserts
a new todo at the top of the list.

The `<fx-trigger>` within the repeat will display a button and allow to delete a todo from the list
with the `<fx-delete>` action.

### The todo list with add and delete

<fx-fore id="todo">
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My Todos
        <fx-trigger class="btn add">
            <button>add</button>
            <fx-insert ref="task" at="1" position="before"></fx-insert>
        </fx-trigger>
    </h1>
    <fx-repeat id="task" ref="task">
        <template>
            <div>
                <fx-control ref="@complete" value-prop="checked" update-event="input">
                    <input class="widget" type="checkbox">
                </fx-control>
                <fx-control class="{@complete}" id="task" ref="."></fx-control>
                <fx-control ref="@due">
                    <input type="date">
                </fx-control>
                <fx-trigger class="btn delete">
                    <button>delete</button>
                    <fx-delete ref="."></fx-delete>
                </fx-trigger>
            </div>
        </template>
    </fx-repeat>
</fx-fore>

This is the barebones of the todo app.
Next chapter will introduce some refinements.

