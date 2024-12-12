---
title: "<fx-upload>"
menuTitle: ""
date: 2024-12-12T11:31:11+01:00
tags: []
weight: 65
---

## Description

Allows to upload data and embed them into an XML document. Support either text or binary content.

Text content will be wrapped in a CDATA element to prevent unexpected changes to the content.

Binary content will be to the bound node of `<fx-upload>` and embedded as base64 encoded string.


> `<fx-upload>` does not currently support usual file uploads to a server. Just use a plain HTML file input for these
> cases.


## Attributes

| Name | Description | Default |
|---|-------------| -------- |
| accept | restricts uploads to a given mediatype | * |
| filename | a XPath binding expression that points to a Node where to store the filename | - |
| mimetype | a XPath binding expression that point to a Node where to store the mediatype |-|
|ref| XPath reference pointing to the bound node | - |


## Examples
* [upload]({{% siteparam "demoUrl" %}}upload.html)
