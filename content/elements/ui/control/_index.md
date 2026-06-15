---
title: "<fx-control>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui, fx-control]
weight: 15   
---
## Description

`fx-control` is no concrete control displayed in the browser but
instead wraps such a control and binds it to a data node in the model with the help of a `ref` attribute.



## Attributes

| Name         | Description | Default |
|--------------|-------------|---|
| as           | 'text' or 'node'. When using 'node' a whole dom tree can be passed to a widget | text |  
| context      | XPath reference pointing to parent context | incopeContext |
| credentials | sets credentials policy - one of 'omit', 'same-origin' or 'include' | same-origin |
| create       | if present on control or anchestor will create non-existing attribute nodes in the data | - | 
| debounce     | optional numeric value in milliseconds to delay input events | - |
| initial      | XPath binding expression referring to data that get passed to Fore control as default instance. Only effective when `url` is specified. | - |
| label        | optional label | - |
| listen-on    | a CSS selector to attach the update event listener to  | element with 'widget' class | - |
| on-demand | boolean attribute which hides control from view | - |
| ***ref***    | XPath reference pointing to the bound node | - |
| shadow       | marker attribute to attach Fore control to shadowDOM instead of lightDOM | - |
| update-event | optional event name when to trigger updating of bound node. | blur |
|              | 'enter' can be used to catch enter key | |
| url          | URL pointing to HTML page containing `fx-fore` element that gets imported as widget | - |
| value-prop   | optional property name used to set the value of the widget (default:'value') | value |

## Attributes on widgets

A widget is an element contained within a `<fx-control>` and must be marked
with a `class="widget"`.

Some attributes might occur on a widget to further control its behavior.

| Name | Description |
| ---- | --- |
| selection | applies to `<select>` elements. If `selection="open"` is given an additional empty `<option>` will be added to allow the empty value.
| data-src | URL of an XML (or JSON) document that is lazily loaded as a lookup-list. The document is loaded into an anonymous `fx-instance` and its root node is bound to the XPath variable `$src` (or `$<data-id>` if `data-id` is given), available to this control's own `ref` and template expressions. |
| data-id | optional name of the XPath variable the document loaded via `data-src` is bound to. Defaults to `src`. |
| data-type | optional type of the document loaded via `data-src`, e.g. `json`. Defaults to `xml`. |
| data-xpath-ns | optional namespace URI used as the XPath default (unprefixed) element namespace when evaluating `ref`/template expressions against `$src`/`$<data-id>`. If omitted, this namespace is derived from the root element of the loaded document. |

## Events

| Name | Description |
|------|-------------|
| init | dispatched once when a control is initialized. Can be used for customization of wrapped widgets. |
| value-changed | dispatched during refresh after the value of the control has changed |
| optional | dispatched during refresh when node has become optional |
| required | dispatched during refresh when node has become required |
| readonly | dispatched during refresh when node has become readonly |
| readwrite | dispatched during refresh when node has become readwrite |
| valid | dispatched during refresh when node has become valid |
| invalid | dispatched during refresh when node has become invalid |
| relevant | dispatched during refresh when node has become relevant |
| nonrelevant | dispatched during refresh when node has become non-relevant |

## Special features

### passing referenced node as node instead of value

With the ´as´ attribute the referenced node will be directly
passed to the widget. This can be useful with control that manipulate 
nodes like e.g. text editors.

### creating selects with an empty option

Sometimes values can and should be empty initially. With `selection="open"` on
the select element it will create such en empty option.

### using on-demand controls

Control may have a boolean `on-demand` attribute which hides them from view unless they
have a value. This allows to create less cluttered  pages in cases where many optional fields 
exist.

Hiding a control is just one side of the medal - with `<fx-control-menu>` on-demand control can be made
visible by the user. See on-demand example

### loading lookup-lists with `data-src`

A widget can load an additional XML (or JSON) document as a lookup-list without
having to declare it as a separate `fx-instance` in the model. Adding `data-src` to
the widget element lazily fetches that document into an anonymous instance and binds
its root node to the XPath variable `$src`, which can then be used in the widget's
own `ref` and template expressions:

```html
<select class="widget" ref="$src//category" data-src="data/decor.xml">
    <template>
        <option value="{@corresp}">{catDesc[@xml:lang = 'en']}</option>
    </template>
</select>
```

If a control needs more than one lookup-list, `data-id` gives each one its own
variable name (`$<data-id>` instead of `$src`):

```html
<select class="widget" ref="$material//category" data-src="data/material.xml" data-id="material">
    <template>
        <option value="{@corresp}">{catDesc[@xml:lang = 'en']}</option>
    </template>
</select>
```

The same `data-src` URL is only ever loaded once and shared between all widgets that
reference it.

#### namespace resolution for `$src` / `$<data-id>`

Unprefixed element names in expressions like `$src//category` are resolved against
an XPath default (element) namespace, which is determined as follows:

* if the loaded document's root element declares a default namespace
  (`xmlns="..."`), that namespace is used automatically - no extra configuration
  needed;
* `data-xpath-ns` on the widget overrides this and explicitly sets the namespace to
  use for `$src`/`$<data-id>`. This is useful when the root element of the loaded
  document is in a different namespace than the elements you actually want to select
  (or has no namespace at all).

If neither applies, unprefixed names resolve against the default instance's
`xpath-default-namespace` as usual.

## using Fore as control
By setting a `url` attribute you can use another [ForeBody](https://jinntec.github.io/fore-docs/glossary/#forebody) as the widget of given control. The `url` is resolved
and will fetch the first `fx-fore` element it finds within that page and embeds it as widget of the control. You can pass in an `fx-instance`
for the loaded widget with `initial` and get the return value with the `return` action. 

## Examples
* [the fx-control element]({{% siteparam "demoUrl" %}}fx-control.html)
* [Actions]({{% siteparam "demoUrl" %}}actions.html)
* [Fore API Demo]({{% siteparam "demoUrl" %}}actions.html)
* [Template Expressions]({{% siteparam "demoUrl" %}}avt.html)
* [Country selector]({{% siteparam "demoUrl" %}}selects.html)
* [Selects]({{% siteparam "demoUrl" %}}selects2.html)
* [Trigger]({{% siteparam "demoUrl" %}}trigger.html)
* [handling credentials]({{% siteparam "demoUrl" %}}submission-credentials.html)
* [on demand controls]({{% siteparam "demoUrl" %}}lab/on-demand.html)





