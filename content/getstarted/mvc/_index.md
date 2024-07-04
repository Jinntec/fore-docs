---
title: "The anatomy of Fore"
date: 2022-05-20T16:08:59+02:00
weight: 2
tags: [basic, mvc, model, ui, actions]
---

Before stepping deeper a basic understanding of the main parts of Fore is helpful.

Fore elements fall into 3 categories:

1. The model elements: the **model** (`<fx-model>`) and its children hold the data and their state, calculate, validate and submit the data. The state
will be reflected in the UI after a refresh.

1. The UI elements: establish a two-way binding between a data value and a control. When the user interacts with a UI element it will trigger ***Actions*** to change
the data in the model or otherwise interact with the UI.

1. The Action elements: **Actions** allow all kinds of interaction with the model or the UI. Examples are setting a value, replacing, inserting or
deleting data , messaging the user, handling keyboard shortcuts, showing a dialog or switching a view. Actions are triggered by events.


