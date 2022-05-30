---
title: "Hello World"
date: 2022-05-20T16:08:59+02:00
weight: 3
tags: [basic, model, instance]
---

What can be learned here:
* the basic structure of Fore
* `<fx-model>` and `<fx-instance>` elements
* using a Template Expression

## Hello World - Step by Step

Each `<fx-fore>` element has a single model.

### 1. Add the model
First step to create a data-bound 'Hello World' example is to add a model.

```
<fx-fore>
    <fx-model></fx-model>
</fx-fore>
```
{{% notice note %}}
The `<fx-model>` is a direct child of the `<fx-fore>` element.
{{% /notice %}}


### 2. Add some data

Not very existing so far so add some data:

```
<fx-fore>
    <fx-model>
        <fx-instance>
            <data>
                <greeting>hello world!</greeting>
            </data>
        </fx-instance>
    </fx-model>
</fx-fore>
```

Data are kept in instances. A model can have as many instances
as needed.

{{% notice note %}}
Currently Fore supports XML and JSON as data formats. However other formats like 
e.g. CSV can be added. 
{{% /notice %}}

### 3. Add some UI

The final step is to add some UI to bind to our data.

```
<fx-fore>
    <fx-model>
        <fx-instance>
            <data>
                <greeting>hello world!</greeting>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My first Fore page</h1>
    <h2>{greeting}</h2>
</fx-fore>
```

Here we use a simple **Template Expression** to output the
data of the node 'greeting'.

A Template Expression is enclosed in curly brackets and binds to some data
node in an instance. You can put them everywhere within the UI of a `<fx-fore>` element
either within text nodes or attributes nodes.



### Live Result:

{{% notice note %}}
The blueish shaded area below shows Fore running inside of this page.
We use live example throughout this documentation.
{{% /notice %}}

<fx-fore>
    <fx-model>
        <fx-instance>
            <data>
                <greeting>hello world!</greeting>
            </data>
        </fx-instance>
    </fx-model>
    <h1>My first Fore page</h1>
    <h2>{greeting}</h2>
    <fx-message event="refresh-done">{greeting}</fx-message>
</fx-fore>






