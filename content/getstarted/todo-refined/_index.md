---
title: "todo refined"
date: 2022-05-20T16:08:59+02:00
weight: 3
tags: [basic, repeat, actions, controls]
---



What can be learned here:
* adding a counter
* insert from a template node
* use `<fx-bind>` to require an value

## Todo refined

In last chapter the bare minimum for the todo app were created.

In this chapter we'd like to make some improvements:
* show a counter for our todos
* hide or show completed todos
* make sure we can handle an empty list

### Extending our data model

Let's add a couple of nodes to our data model to cover our objectives.

```
<data>
    <task complete="false" due="2022-06-05">Make tutorial part 1</task>
    <task complete="false" due="2022-06-15">Pick up Milk</task>
    <template>
        <task complete="false" due="">new task</task>
    </template>
    <showclosed>false</showclosed>
</data>
```

### Adding the counter

Starting with the counter we added this above the repeat 

```
    <div class="info">
        You have {count(task)} completed tasks
    </div>
```

The Template Expression will output the number of task nodes in the data.

{{% notice note %}}
`count()` is an built-in [XPath 3.1](https://www.w3.org/TR/xpath-31/) function we're using to get the number of todos. XPath
offers a big library of functions. 
{{% /notice %}}

### Fixing our repeat

If you've played with the example from last chapter and have deleted all 
todos and trying to re-add one you have run into problems. It simply refuses
to create a new repeat entry.

This is due to the default behavior of `<fx-insert>`. It tries to use
the last item in the list as a template for insertion. If there's none left,
the nodeset is empty and the `<fx-insert>` will do nothing.

The `origin` attribute handles this sitution and allows us to bind to a template
node to use for the insert.

By changing the trigger from 

```
<fx-trigger class="btn add">
    <button>add</button>
    <fx-insert ref="task" at="1" position="before"></fx-insert>
</fx-trigger>
```

into

```
<fx-trigger class="btn add">
    <button>+</button>
    <fx-insert ref="task" at="1" position="before" origin="template/task"></fx-insert>
</fx-trigger>
```

Now the insert will evaluate the `origin` attribute and take that node
to insert into the list.

By using this technique you can also apply some defaults for new entries e.g. 
a todo will now be `complete="false"` by default.

### Adding constraints

Certainly at some point you'd like to save your todo list and it makes not much
sense to have a todo without a text.

Let's create a constraint for that by introducing a bind element:
```
<fx-bind ref="task" required="true()"></fx-bind>
```

The `required` attribute takes an boolean XPath expression which will 
automatically be applied by the model and re-evaluated whenever this is required.

{{% notice note %}}
Fore uses XPath to bind nodes or make calculations. To learn more about XPath and play with it, have a look
at <a href="https://xpath.playground.fontoxml.com/" target="_blank">fontoXPath playground</a>
{{% /notice %}}

A bind applies a constraint on a bind node or applies a calculation to it. It may also have an alert 
message when a constraint fails.

Add the bind to the model somewhere.

{{% notice note %}}
Tip: though not strictly necessary it makes sense to group your `<fx-instance>`, 
`<fx-bind>`,`<fx-submission>` and `<fx-function>` elements for a better
overview when things get more complex.
{{% /notice %}}


```
<fx-fore>
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
                <template>
                    <task complete="false" due="">new task</task>
                </template>
                <count>1</count>
                <showclosed>false</showclosed>
            </data>
        </fx-instance>
        <fx-bind ref="task" required="true()"></fx-bind>
    </fx-model>
    <h1>Todo</h1>
    <fx-trigger class="btn add">
        <button>+</button>
        <fx-insert ref="task" at="1" position="before" origin="template/task"></fx-insert>
    </fx-trigger>
    <div class="info">
        You have {count(instance()/task[@complete='true'])} completed tasks
    </div>
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

## Result
<fx-fore id="todo">
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
                <template>
                    <task complete="false" due="">new task</task>
                </template>
                <count>1</count>
                <showclosed>false</showclosed>
            </data>
        </fx-instance>
        <fx-bind ref="task" constraint="string-length(.) > 0" alert="what's your todo?"></fx-bind>
    </fx-model>
    <h1>Todo
        <fx-trigger>
            <button>add</button>
            <fx-insert ref="task" at="1" position="before" origin="template/task"></fx-insert>
            <fx-refresh></fx-refresh>
        </fx-trigger>
    </h1>
    <div class="info">
        You have {count(instance()/task[@complete='true'])} completed tasks
    </div>
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

Now you can delete all entries and create new ones afterwards.