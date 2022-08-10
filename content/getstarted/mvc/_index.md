---
title: "The anatomy of Fore"
date: 2022-05-20T16:08:59+02:00
weight: 2
tags: [basic, mvc, model, ui, actions]
---

Before stepping deeper a basic understanding of the main parts of Fore is helpful.

Fore uses a classical Model-View-Controller (MVC) architecture.

![MVC](/images/mvc.svg)

There are 3 basic things to remember:
1. The **model** (`<fx-model>`) holds the data and their state. This state
will be used during refresh to apply changes to the UI.

1. When the user interacts with a page the **UI** will trigger Actions to change
the data in the model. 

1. **Actions** will do the actual mutation of the data like setting a value, replacing, inserting or
deleting a data node. But not all actions mutate the model - there are also actions
for messaging the user, showing a dialog or switching a view.

{{% notice note %}}
The term 'data node' does not mean it needs to be a DOM node. It can also point 
to a JSON property or some other data item.
{{% /notice %}}

