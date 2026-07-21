---
title: "<fx-repeat>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, ui, fx-repeat, repeat]
weight: 45
---

## Description

Repeats template for each node of the referenced nodeset.

For each data node in the referenced nodeset one `<fx-repeatitem>` element
will be created that will contain the evaluated template as content.


## Attributes

| Name | Description | 
|------|-------------| 
| id | identifier for repeat |
| ***ref*** | XPath reference pointing to the bound node | - |
| size | Caps how many `fx-repeatitem` elements are materialized from the (always-complete) bound nodeset. Without `virtual`, this is a growing prefix cap: a trailing sentinel reveals the next `size` items via `IntersectionObserver` as the user scrolls, and once rendered, rows are never un-rendered. With `virtual`, `size` instead becomes the size of a sliding window. Omit for full, uncapped rendering (the default). | - |
| virtual | Opt-in true windowed virtualization, only meaningful together with a finite `size`. Instead of an ever-growing prefix, the DOM stays bounded at roughly `size` rows regardless of nodeset size: scrolling down appends rows below and evicts rows from the top; scrolling up prepends rows above and evicts from the bottom. `virtual` without `size` is ignored (behaves as fully uncapped). | - |

## Progressive rendering and virtualization

`size` only limits *DOM materialization*. The logical nodeset - and therefore `index()`, `iterate` actions, and explicit `fx-bind` model semantics (`calculate`, `constraint`, `required`, `readonly`, `relevant`) - always covers every item, regardless of how many rows are currently rendered. Programmatic or keyboard navigation to an index beyond the currently rendered window (e.g. via `setIndex`, an `index('id')`-driven dependent, or an insert/append past the window) materializes rows on demand: without `virtual`, it front-fills up through the target row; with `virtual`, it performs a hard jump - the current window is discarded and a fresh one is rendered starting at the target index, resetting scroll position to the top of that window.

Adding `virtual` alongside `size` turns on a sliding window: only about `size` rows are ever in the DOM, no matter how large the nodeset is. Eviction never estimates row height - it measures the actual height of the rows being removed and corrects the scroll position by that exact amount, so the visible content doesn't jump. One consequence: the native scrollbar no longer represents absolute position in the full dataset (it behaves like a bounded infinite-scroll list, not "thumb at 45% of 10,000 rows"). Item recycling (reusing existing `fx-repeatitem` subtrees instead of destroying/recreating them) is a possible later enhancement.

```html
<fx-repeat ref="item" size="50" virtual>
  <template>
    ...
  </template>
</fx-repeat>
```

## Recursive templates

`ref` is evaluated relative to the current context, so a statically nested
`fx-repeat` (one written by hand inside another's template) already renders
correctly at any fixed depth. For a self-similar tree of *unknown* depth
(file trees, org charts, threaded comments), use
[`fx-repeat-ref`]({{% ref "/elements/ui/repeat-ref" %}}) instead of writing
out a depth-capped chain by hand:

```html
<fx-repeat id="tree" ref="folder|file" recursive="true">
  <template>
    <li>
      <span>{@name}</span>
      <ul>
        <fx-repeat-ref></fx-repeat-ref>
      </ul>
    </li>
  </template>
</fx-repeat>
```

`<fx-repeat-ref>` re-applies the enclosing template to the current node's own
matching children, one level deeper each time, terminating naturally once a
node has no more matching children. See its own page for the `ref` override
attribute and further detail.

## Drag and drop

Set `draggable="true"` and `drop-target="<this repeat's id>"` on the
**template** (not on `fx-repeat` itself) to let items be reordered or moved
between repeats by drag and drop - see the
[Kanban Board]({{% siteparam "demoUrl" %}}kanban.html) and
[Drag and Drop]({{% siteparam "demoUrl" %}}drag-drop-interface.html) demos,
and [`fx-droptarget`]({{% ref "/elements/ui/droptarget" %}}) for dropping onto
non-repeat targets.

By default, a drop is accepted when the dragged item and the drop target
share the same nearest ancestor element carrying an `id` - a plain string
comparison, not real data parentage. This is what lets a Kanban card be
dragged between different columns of one repeat; but for two
*structurally identical* repeats at the same depth (notably: every level of a
recursive tree built with `fx-repeat-ref`, since every level shares one
template and therefore one literal `id`), it cannot tell "true siblings under
the same real parent" apart from "cousins at the same depth under a different
parent."

Add `drop-scope="parent"` to the template to switch the check to real parent
equality (the dragged item's and the drop target's actual bound data node
having the same parent), independent of `id`:

```html
<fx-repeat id="tree" ref="folder|file" recursive="true">
  <template draggable="true" drop-target="tree" drop-scope="parent">
    ...
  </template>
</fx-repeat>
```

`drop-scope="parent"` is opt-in; existing repeats that don't set it keep
today's `id`-equality behavior unchanged. See the
[Recursive tree]({{% siteparam "demoUrl" %}}repeat-recursive.html) demo, which
sets it on a recursive template to block drags between structurally identical
sibling branches, and the standalone
[Drop scope]({{% siteparam "demoUrl" %}}repeat-drop-scope.html) demo.

## Events

| Name | Description | Details
|------|-------------|--- |
| item-created | dispatched when a new repeat entry is created | 'path' - a canonical xpath <br> 'index' - the index of the new item |
| path-mutated | dispatched when repeat nodeset changes | 'path' - the mutation path <br> 'index' - the index of the changed repeat item.
| no-template-error | dispatched when there's no template defined | 'id' - the repeat id |


## Examples

* [API Demo]({{% siteparam "demoUrl" %}}api.html)
* [docbook Bibliography]({{% siteparam "demoUrl" %}}docbook-bibliography.html)
* [insert]({{% siteparam "demoUrl" %}}insert.html)
* [todo]({{% siteparam "demoUrl" %}}nested-todo.html)
* [Project Task planner]({{% siteparam "demoUrl" %}}project.html)
* [Atomic repeat]({{% siteparam "demoUrl" %}}repeat-atomic.html)
* [repeat in switch]({{% siteparam "demoUrl" %}}repeat-in-switch.html)
* [repeat sequence]({{% siteparam "demoUrl" %}}repeat-sequence.html)
* [the while attribute]({{% siteparam "demoUrl" %}}while.html)
* [Recursive tree]({{% siteparam "demoUrl" %}}repeat-recursive.html)
* [Drop scope]({{% siteparam "demoUrl" %}}repeat-drop-scope.html)



