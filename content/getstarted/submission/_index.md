---
title: "Submissions"
menuTitle: "loading and sending data"
date: 2021-12-14T17:41:11+01:00
tags: [getstarted, submission]
chapter: false
---

Ok, nice - we have a todo list that will be gone when we reload the browser 
of leave the page.

<fx-fore id="todo">
    <fx-model id="record">
        <fx-instance>
            <data>
                <task complete="false" due="2022-06-05">Make tutorial part 1</task>
                <task complete="false" due="2022-06-15">Pick up Milk</task>
                <template>
                    <task complete="false" due="">new task</task>
                </template>
            </data>
        </fx-instance>
        <fx-bind ref="task" constraint="string-length(.) > 0" alert="what's your todo?"></fx-bind>
    </fx-model>
    <h1>Todo
        <fx-trigger class="btn add">
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

## Adding a submission

We need a way to store our data. Let's add a submission which 
will go into our model

```
<fx-submission id="save"
               method="post"
               url="#echo"
               replace="instance"
               instance="todo-list">
</fx-submission> 
```

{{% notice note %}}
Due to technical limitations on this static site we use the builtin
'#echo' target for this tutorial that will just return the data it gets in and replaces 
another instance with it. This is to simulate what is usually happening when sending data via http. 
{{% /notice %}}

What does this do?
1. We need to add an `id` to identify a submission
1. This submission will send a POST request
of the instance data to the URL '#echo'
1. The response will replace the instance. 
1. The instance to be replaced is 'todo-list' 

## Triggering the save submission 
To trigger a save operation you usually want a button.

```
    ... UI ...
    <fx-trigger>
        <button>Save</button>
        <fx-send submission="save"></fx-send>
    </fx-trigger>
``` 

Put together

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
        <fx-instance id="saved-list">
            <data></data>
        </fx-instance>
        <fx-bind ref="task" constraint="string-length(.) > 0" alert="what's your todo?"></fx-bind>
        <fx-submission id="save"
                       method="post"
                       url="#echo"
                       replace="instance"
                       instance="saved-list">
           <fx-message event="submit-done">your todo list has been saved</fx-message>
        </fx-submission> 
    </fx-model>
    <h1>Todo
        <fx-trigger class="btn add">
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
    <fx-trigger class="save">
        <button>Save</button>
        <fx-send submission="save"></fx-send>
    </fx-trigger>
    <fx-inspector open></fx-inspector>
</fx-fore>

Watch the 'Data Inspector' on the right. Intially there will be 2 data instances listed by their id.
{{% notice note %}}
Data Inspector is a tool that helps during development to see the live content of your data instances. 
The instance live separate from the DOM and therefore cannot be seen in their actual state by inspecting
with developer tools.
You can just add it within any `<fx-fore>` element.
{{% /notice %}}

After hitting the 'Save' button the instance 'todo-list' will be identical to the 'default' instance.

This means that our submission has been executed and has send its data to the '#echo' submission, that gets back the 
same data and replaced the 'saved-list' instance.

## Messsaging the user

You may have noticed a message in the lower left after hitting 'save'.

Let's add the missing line i omitted from above code.
```
<fx-submission id="save"
               method="post"
               url="#echo"
               replace="instance"
               instance="saved-list">
   <fx-message event="submit-done">your todo list has been saved</fx-message>
</fx-submission> 
```

This adds a `<fx-message>` element to the submission that will react to the 'submit-done' event
that is fired when a submission successfully returned. 

The message element defaults to a toast message
that disappears after a delay. 

With the `event` attribute the message action attaches to its parent element and reacts to 'submit-done' in this case. 

{{% notice note %}}
This technique is used all over Fore to attach event handlers that in turn will run an action.
{{% /notice %}}

## Where to go from here?

This tutorial only touched the surface of the possibilities. To further learn about Fore the following 
resources are recommended:

* The <a href="https://jinntec.github.io/Fore/doc/demos.html" target="_blank">Demos</a>. Fore evolves along the demos and they will show the latest in live running examples along 
with the source code. Running through them will give you an impression of what can be done and how.
* The [Element Reference](../../elements/) describes all Fore elements in more detail and also links to 
the live demos.
* For those interested in the inner workings of Fore the [Architecture](../../architecture/) section should have some answers.





