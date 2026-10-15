---
title: "<fx-bind>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, model, fx-bind]
weight: 5
---

## Description

The `fx-bind` element attaches constraints and calculations to instance nodes.
  
## Attributes

| Name | Description | Default |
|------|-------------| --- |
| alert | used to specify a message to be displayed when constraints fail | - |
|ref | XPath pointing to node(s) the bind is attaching to | - |
| calculate | XPath expression to be calculated. Result will become value of node(s) referenced by `ref` | - |
| initial | XPath expression evaluated once during model initialization, before any `calculate`. Overwrites the existing value of node(s) referenced by `ref`; does not make the node readonly. Nodes added later (e.g. inserted rows) get their initial value once when they first enter the model. If evaluation fails the value becomes the empty string. | - |
| constraint | boolean XPath expression to determine validity of node(s) | true |
| readonly | boolean XPath expression to determine readonly/readwrite state | false |
| relevant | boolean XPath expression to determine relevant/non-relevant state | true |
| required | boolean XPath expression to determine required/optional state | false |
| type | datatype - reserved for future versions | string |

### The `initial` property

`initial` follows [XForms 2.0](https://www.w3.org/community/xformsusers/wiki/XForms_2.0#The_initial_Property): it is a
one-time calculation that runs while the model is initialized, before any `calculate`. Unlike `calculate` it
overwrites the value only once and leaves the node editable.

```html
<fx-bind ref="balance" initial="0" calculate="../credit - ../debit"></fx-bind>
```

Models without any `initial` do not pay for the feature.

#### Using `initial` with JSON instances

`initial` works on nodes of `type="json"` instances. Differences and limits compared to XML:

* **Typed result:** the result keeps its type, `initial="10"` stores the number `10`, not the string `"10"`.
  A sequence is reduced to its first item; an empty result or an error stores the empty string.
* **Context item:** for expressions that are not a path, the context item is the **raw value** of the bound node
  (string, number or boolean, or a map/array for objects and arrays). `.` yields that value and `.?key` looks into
  an object.
* **Paths:** an expression that is a plain path of simple steps is resolved against the JSON tree. Supported are
  `.`, `..`, `*`, `name`, `self::*`, `parent::*`, `child::*`, `child::name`, a leading `/` for the root, and one
  1-based numeric predicate per step: `../label`, `*[2]`, `/count`.
* **Lookups:** `?key` and `instance('id')?key` lookups work, also inside larger expressions such as
  `instance('j')?count + 1` or `string-length(instance('j')?label)`.
* **Not supported:** axis steps inside functions or operators (`string(../label)`, `../a + ../b`), `//`,
  predicates other than a number (`*[a=1]`), and the other axes (`descendant::`, `following-sibling::`, ...). Use
  `?key` lookups for those - `instance('j')?label` instead of `../label` inside a larger expression. An unsupported
  path is reported with an `error` event on the model (message: "... is not supported on JSON nodes") and evaluates
  to the empty string.

The same evaluation rules apply to the other bind properties (`calculate`, `relevant`, `readonly`, `required`,
`constraint`) on JSON nodes.

```html
<fx-instance id="j" type="json">{"count": 5, "label": "x"}</fx-instance>
<fx-bind ref="instance('j')?count" initial="10"></fx-bind>
<fx-bind ref="instance('j')?label" initial="concat('a', 'b')"></fx-bind>
<fx-bind ref="instance('j')?next" initial="instance('j')?count + 1"></fx-bind>
```

## Events

none

## Examples

* [nested Binding]({{% siteparam "demoUrl" %}}binding-nested.html)
* [Binding]({{% siteparam "demoUrl" %}}binding.html)
* [Hello]({{% siteparam "demoUrl" %}}body.html)
* [Simple Calculate]({{% siteparam "demoUrl" %}}calc-order.html)
* [todo]({{% siteparam "demoUrl" %}}nested-todo.html)
* [Recalculate]({{% siteparam "demoUrl" %}}recalculate.html)
* [Revalidation]({{% siteparam "demoUrl" %}}revalidate.html)
* [Submission Relevance Processing]({{% siteparam "demoUrl" %}}submission-relevance.html)

