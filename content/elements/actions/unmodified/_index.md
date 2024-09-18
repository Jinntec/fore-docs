---
title: "<fx-unmodified>"
menuTitle: ""
date: 2024-09-18T14:41:24+02:00
weight: 180
tags: []
---

### Description

This action can be used in conjunction with a page exit confirmation to reset the
modified state of a `fx-fore` element.

To display a confirmation dialog before leaving a page which has changed data, Fore uses the
`show-confirmation` boolean attribute. If present the confirmation will be displayed 
before navigating.

To reset data to clean state (e.g. after a saving operation) this action can be called and
suppresses the confirmation until data are modified again by user interaction.

Typical use case would be to call it from a submission that stores data on a server:
```
<fx-submission id="save" url="myserver/docs/" method="post" ...>
    <fx-unmodifed event="xforms-submit-done"></fx-unmodified>
</fx-submission>
```

When the submission returned successfully the 'modified' state is reset to 'clean'.


### Attributes

none

## Events

none

### Examples
* [showing page exit confirmation]({{% siteparam "demoUrl" %}}beforeunload.html)

