---
title: "<fx-var>"
date: 2026-07-11T10:00:00+01:00
tags: [elements, fx-var]
weight: 3
---

## Description

Declares a named variable. The `value` expression is evaluated and the result
can be used in any following XPath expression as `$name`.

```html
<fx-var name="discount" value="price * 0.1"></fx-var>
<fx-output value="price - $discount"></fx-output>
```

Variables help to avoid repeating the same expression in several places and to
give intermediate results a readable name.

## When variables are evaluated

A variable is **not** updated the moment its data changes. Instead it is
(re)evaluated at fixed points, depending on where it is declared:

| Declared | Evaluated |
|------|-------------|
| outside of model and actions (a *UI variable*) | on every refresh, in document order |
| inside `<fx-model>` (a *model variable*) | before the model updates (rebuild/recalculate), so it can be used in `<fx-bind>` facets like `calculate` |
| inside an action or `<fx-trigger>` (an *action variable*) | at its position between the sibling actions, once per execution — an action after the variable sees its value, an action before it does not affect it yet. With `iterate` or `while` the variable is re-evaluated on each iteration |

Between these points the variable keeps its value like a snapshot: deleting
nodes it holds or changing values it was computed from does **not** change the
variable until its next evaluation point.

When a UI variable gets a new value during a refresh, elements whose `ref` or
`value` expressions use that variable are refreshed as well — so outputs,
repeats etc. always show values consistent with the current variable values.

## Scope

A variable is visible to its **following siblings and their descendants** —
not to elements before it, and not to its own `value` expression. Variables
can build on each other as long as they are declared in order:

```html
<fx-var name="base" value="xs:integer(counter)"></fx-var>
<fx-var name="derived" value="$base * 10"></fx-var>
```

Declaring the same variable name twice dispatches a `binding-error`.

## Implicit instance variables

Every instance is available as a variable automatically: `$default` points to
the default instance and `$<instance-id>` to each instance with an explicit
`id`. These exist without any `<fx-var>` declaration. An explicit `<fx-var>`
with the same name overrides the implicit binding.

These implicit variables always follow the current instance data. When the
data of an instance is replaced — e.g. by a submission with
`replace="instance"` or by `<fx-reset>` — `$default` and `$<instance-id>`
point to the new data afterwards.

## Events

| Name | Description |
|------|-------------|
| binding-error | dispatched when a variable name is declared more than once |

## Attributes

| Name | Description | Default |
|------|-------------| -------- |
| ***name*** | the variable name, used as `$name` in expressions | - |
| ***value*** | XPath expression computing the value of the variable | - |

## Examples

* <a href="{{% siteparam "demoUrl" %}}variables.html" target="_blank">Variables</a>
* <a href="{{% siteparam "demoUrl" %}}nested-default-vars.html" target="_blank">Nested default variables</a>
