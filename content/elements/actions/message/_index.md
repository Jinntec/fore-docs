---
title: "<fx-message>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions, message]
weight: 80
---

## Description

Display a message to the user.

## Attributes

| Name | Description | default |
|------|-------------| ------ |
| level | 'modal', 'modeless' or 'ephemeral' | ephemeral |
| | 'modal' - modal dialog window | |
| | 'sticky' - sticky popup message  | |
| | 'ephemeral' - auto-closing popup message  | default |
| appearance | how the message looks, e.g. 'toast' or 'banner'. Adds the CSS class `appearance-<name>` | toast |
| | 'toast' - small box in the corner (default look) | |
| | 'banner' - full-width bar at the top with a close button | |
| value | XPath expression which resolves to message | |

### Appearances

`level` says how important a message is, `appearance` how it is presented; both can be combined,
e.g. `<fx-message level="error" appearance="banner">`. Every shown message gets the class
`appearance-<name>`, so it can be styled from the page's CSS (`.toastify.appearance-banner { … }`).

Custom appearances can be registered in JavaScript and styled via their class:

```js
FxFore.registerMessageAppearance('corner-note', { gravity: 'bottom', position: 'right', duration: 8000 });
```

An unknown appearance logs a warning and falls back to the default look.


## Events

none

## Examples

* [fx-message]({{% siteparam "demoUrl" %}}fx-message.html)
* [actions]({{% siteparam "demoUrl" %}}actions.html)
* [Binding]({{% siteparam "demoUrl" %}}binding.html)
* [the delay attribute]({{% siteparam "demoUrl" %}}delay.html)
* [fx-control]({{% siteparam "demoUrl" %}}fx-control.html)
* [Hello World]({{% siteparam "demoUrl" %}}hello-fonto.html)
* [the if attribute]({{% siteparam "demoUrl" %}}if.html)
* [instances]({{% siteparam "demoUrl" %}}instances.html)
* [lazy modelItem creation during UI init]({{% siteparam "demoUrl" %}}lazy.html)
* [the while attribute]({{% siteparam "demoUrl" %}}while.html)



