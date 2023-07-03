---
title: "Elements"
date: 2021-12-14T17:41:11+01:00
weight: 2
chapter: true
---

# Fore Elements

Fore Elements are a set of Web Components that allow to build
feature-complete HTML-driven applications. 

It can be used to build small components or large and complex applications.

All Fore component use the prefix **'fx-'** to identify them as a 
related set of Web Components.

Fore elements allow to perform all various tasks that are needed for a
full state-driven application like (not limited to):

* loading and holding data
* sending and receiving data
* applying constraints to data
* changing of data
* data-binding controls

All functionality is fully available without writing any JavaScript.

Elements fall into 3 categories:
* Model Elements
* UI Elements
* Action Elements

## Model Elements

Fore uses a model to hold all data sources, data-constraints, calculations
and submissions.

The model (`fx-model`) is a 'blind' element. It does not appear on screen.

## UI Elements

Fore UI Elements are generic - they allow to bind a part of an HTML page
to data being hold by `fx-instance` elements.

They wrap the actual controls they are bound to. The many examples show
how this is done. 

## Action Elements

With Actions you can insert or delete data, change values, show/hide dialogs etc.

Actions that update data will automatically trigger the necessary updates of 
the UI and keep the model in sync.
