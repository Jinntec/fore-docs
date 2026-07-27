---
title: "<fx-repeat-ref>"
menuTitle: ""
date: 2026-07-21T12:00:00+02:00
tags: [elements, ui, fx-repeat, repeat, recursive]
weight: 47
---

## Description

`fx-repeat-ref` is a placeholder used inside an [`fx-repeat`]({{% ref "/elements/ui/repeat" %}})
template to recurse into a data node's own matching children - the same idea as
XSLT's `apply-templates`. It lets one template render an arbitrary-depth,
self-similar tree (file/directory trees, org charts, threaded comments, nested
categories, outline structures) instead of a hand-written, depth-capped chain
of nested `fx-repeat` elements.

Place `<fx-repeat-ref>` anywhere inside the nearest ancestor `fx-repeat`'s
template. On connect, it synthesizes a new `fx-repeat` bound to that same
`ref` (or an explicit override, see below), wraps a clone of the ancestor's
template around it, and replaces itself with that new repeat. The new repeat
then goes through the same lifecycle as any other: if its own template
contains another `<fx-repeat-ref>`, recursion continues one level deeper,
scoped to the current item via the usual nested-repeat context resolution.
Recursion terminates naturally wherever a node has no more matching children -
no depth check or `max-depth` attribute is needed for correctness.

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

against

```xml
<data>
  <folder name="src">
    <folder name="ui">
      <file name="fx-repeat.js"/>
    </folder>
    <file name="index.js"/>
  </folder>
  <folder name="docs">
    <file name="README.md"/>
  </folder>
</data>
```

renders the whole tree, any depth, from a single template.

## Attributes

| Name | Description | Default |
|------|-------------|---------|
| ref  | Overrides the XPath used for the synthesized nested repeat. Without it, the nearest ancestor `fx-repeat`'s own `ref` is reused. Useful when a generation should switch to a different child axis (e.g. a `folder` template recursing into `file` children). | ancestor repeat's `ref` |

The `recursive="true"` attribute on the enclosing `fx-repeat` is documentation
only - the recursion itself is driven purely by the presence of
`<fx-repeat-ref>` in the template - but setting it is recommended so the
intent is clear to readers of the markup.

## Drag and drop across recursion levels

Because every synthesized repeat is materialized from the same template, each
recursion level emits the same literal `id` on its `fx-repeat`/`fx-repeatitem`
pair - but since a synthesized level never gets an explicit `id` of its own
(see below), the nearest-ancestor-`id` walk that Fore's default drag/drop
scoping performs passes straight through every recursion level and lands on
the one real `id` on the outermost `fx-repeat`. That means, by default, every
node anywhere in the tree is in the same drop scope - a node can be dragged
out of one branch and dropped into any other, including a structurally
identical one. The [Recursive tree]({{% siteparam "demoUrl" %}}repeat-recursive.html)
demo relies on exactly this for its file-browser-style tree: any file can be
dragged into any folder, anywhere.

If that's *not* what an app wants - a tree editor where cross-branch drags
should be rejected, say - add `drop-scope="parent"` to the template (see the
"Drag and drop" section on the [`fx-repeat`]({{% ref "/elements/ui/repeat" %}})
page) to scope drops to each node's real parent instead, regardless of
recursion depth; see the standalone
[Drop scope]({{% siteparam "demoUrl" %}}repeat-drop-scope.html) demo.

**Dropping into an empty branch:** dropping onto an existing node inserts the
dragged node as its sibling - so the natural way to drop *into* a folder-like
node is to drop onto one of its existing children. A node with no children
yet has nothing to drop onto for that unless its own synthesized nested
`fx-repeat` (which is *itself* a valid drop target - it means "append into
this repeat") is given a real, non-zero-size box. Left at the browser's
inline default, an empty `fx-repeat` collapses to nothing, and there is
nothing left to hit-test a drop against. Give it a block-level `display` and
some `min-height` (see the `ul.tree > fx-repeat` rule in the
[Recursive tree]({{% siteparam "demoUrl" %}}repeat-recursive.html) demo's
`<style>`) so an emptied-out branch stays droppable.

## Selection and `index()`

Synthesized nested repeats never get an explicit `id`, and this is
deliberate, not an oversight: `index('id')` is not a flat lookup by that
`id` - it's context-relative whenever more than one element could share it.
Internally it walks up from the *calling expression's own*
`ancestor::fx-repeatitem` chain and returns whichever candidate is contained
in the nearest enclosing one. That's workable for a hand-nested, non-recursive
chain of repeats reusing one `id` per generation, evaluated from *inside* the
tree - but it breaks down for anything evaluated *outside* any relevant
`fx-repeatitem` ancestor chain (a master/detail panel elsewhere on the page,
say), where there's no ancestor chain to disambiguate and, with several
same-id candidates, no single global match either. In that situation
`index()` silently falls back to `1` rather than erroring.

With `<fx-repeat-ref>` this is even more clear-cut: synthesized repeats have
no `id` at all, so there's nothing for `index()` to resolve past the single
author-written root - it can only ever report that root repeat's own
top-level active row, never anything about a deeper recursion level. There is
no "flattened" or "virtualized" index that would fix this: `index()`'s whole
design is the current row of *one specific* repeat instance, resolved
relative to where you're standing, not a position in a global ordinal space
- and the set of synthesized repeats is re-derived from data shape on every
render, so there's no stable ordinal to assign one to in the first place.

If you need to track or visually mark "the selected node" across a recursive
tree - especially from outside the tree, e.g. a property/detail panel - don't
reach for `index()`. Set a marker attribute on the bound data node itself
instead:

```xml
<fx-setattribute ref="." name="ui-selected" value="true"></fx-setattribute>
```

and read it back with `//*[@ui-selected='true']` (plus a matching CSS
selector for the visual highlight). This resolves identically no matter where
it's evaluated from, and needs no per-repeat `id` at all - it's keyed by the
data node, not by any repeat instance or its position.

Similarly, use `fx-insertchild parent="."`-style, context-relative actions to
insert children at any depth, rather than an `id`-targeted `fx-append`.

## Notes

* `fx-repeat-ref` removes itself from the DOM as soon as it connects; it never
  appears in a rendered tree and takes no part in the update cycle itself.

## Examples

* [Recursive tree]({{% siteparam "demoUrl" %}}repeat-recursive.html)
