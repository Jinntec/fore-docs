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
| id | id of the instance for addressing in refs | default |
| src | url to load instance from via http get | |
| type | 'xml' or 'json' or 'html' are supported by now | xml |
| xpath-default-namespace | namespace to be used with unprefixed XPathes | emtpy |


## Examples

* <a href="{{% siteparam "demoUrl" %}}03-instances.html" target="_blank">Instances</a>
* <a href="{{% siteparam "demoUrl" %}}04-instances.html" target="_blank">Instance super powers</a>
* <a href="{{% siteparam "demoUrl" %}}controls/fx-output.html" target="_blank">the fx-output element</a>


