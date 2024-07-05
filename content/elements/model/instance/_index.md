---
title: "<fx-instance>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, model, fx-instance]
---

## Description

Holds the data of the model. A `fx-model` may have as many `fx-instance` elements as
necessary.



## Attributes

| Name | Description | default |
|------|-------------|------- |
| credentials | sets credentials policy - one of 'omit', 'same-origin' or 'include' | same-origin |
| id | id of the instance for addressing in refs | default |
| shared | boolean attribute to signal that the instance is shared with nested Fore elements | |
| src | url to load instance from via http get. This may have static params but cannot use dynamic parameters. See fx-submission for if required. | |
| type | 'xml' or 'json' or 'html' are supported by now | xml |
| xpath-default-namespace | namespace to be used with unprefixed XPathes | emtpy |

## Using multiple instances

When using multiple instances you must add an `id` attribute to each instance that is NOT the first in document order. The first is known as the [default instance](https://jinntec.github.io/fore-docs/glossary/#default-instance) and doesn't need an explicit id but can be accessed with `instance()` or `instance('default'). 

You can still however add an id (e.g. 'myCustomId') if you like and `instance()` or `instance('myCustomId')` will return it. 

## Inline versus external data

A data structure can be given inline or be loaded via the `src` attribute. However there are important limitations of inline instances to be mentioned:
* tagnames are not context-sensitive
* There are no self-closing elements as in XML

If your require these features you have to create an external XML file and load it with the `src` attribute. This gives you a proper XML document.


## The `src` attribute

When static data files shall be loaded you can use the `src` attribute which may also have some static attributes. However, as instance data can
be accessed not before all have been loaded you cannot have dynamic parameters that refer to other nodes.

If that is required you have to use the `fx-submission` element and use a 'get' request with `replace="instance"` to load the data. The submission is then usually fired on `model-construct-done`. Examples can be found in the demos.

## Shared instances

By adding an `shared` attribute to an `<fx-instance>` that instance is shared with nested `<fx-fore>` elements and can be accessed and mutated as usual. 

This can be used if multiple nested Fore elements represent different views but you want to share some common data.

Another possible use case is to separate the model from the UI part and put them in different files for dynamic assembly at runtime (see documentation under 'modularization').


## URI Schemes

In addition to 'http', 'https' further URI schemes are:
  * '#querystring' will create a XML structure for the URL parameter of the page
  * 'localStore:[key]' to read some data from browsers' localstorage
  
  
## Examples

* <a href="{{% siteparam "demoUrl" %}}03-instances.html" target="_blank">Instances</a>
* <a href="{{% siteparam "demoUrl" %}}04-instances.html" target="_blank">Instance super powers</a>
* <a href="{{% siteparam "demoUrl" %}}controls/fx-output.html" target="_blank">the fx-output element</a>
* <a href="{{% siteparam "demoUrl" %}}submission-localStore.html" target="_blank">localStore</a>
* <a href="{{% siteparam "demoUrl" %}}submission-credentials.html" target="_blank">Handling credentials</a>
* <a href="{{% siteparam "demoUrl" %}}shared-instances.html" target="_blank">Shared instances</a>
  


