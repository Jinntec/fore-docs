---
title: "<fx-load>"
date: 2023-01-16T12:00:00+01:00
tags: [elements actions, load]
weight: 70
---

## Description

Loads some content into a page, open a new tab with content or replaces
current browser window with content.

Content may be loaded from `url` or be specified inline surrounded with a `template` element.

If the HTML being loaded contains a `fx-fore` element it will be extracted from the page and used as content to be inserted.

## Attributes

| Name      | Description                                  | default |
|-----------|----------------------------------------------|---------|
| attach-to | '_self', '_blank' or idref prefixed with '#' | _self   |
| await     | eventname to await from templated content    | -       |
| url       | URL to load content from                     |         |

### The `await` attribute

Sometimes if you load a component with `fx-load` and the component has some initialization to do, you might want to wait 
for a certain event dispatched by that component before moving on. `await` will make sure this event fires before the load action
becomes effective.

## Events

| Name       | Description                                 |
|------------|---------------------------------------------|
| url-loaded | dispatched after successful load of content |


## Examples

* [load]({{% siteparam "demoUrl" %}}load.html)


### 'Unloading' a section

With load you can also delete parts of the DOM and replace them with an empty element.

This is useful to reset a formerly loaded section again when you're done with it.

```
<fx-load attach-to="#htmlout">
  <template><div></div></template>
</fx-load>
```

## Examples

* [The load action]({{% siteparam "demoUrl" %}}load.html)

