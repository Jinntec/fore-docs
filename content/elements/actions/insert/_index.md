---
title: "<fx-insert>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions]
---

## Description

Action to insert node(s) into instance data.

## General Binding Attributes
| Name | Description |
|------|-------------|
| ***ref*** | XPath pointing to node(s) the bind is attaching to |

## Attributes

| Name | Description | Default |
|------|-------------| --------|
| at | index position in nodeset where to insert new node(s) | 0 |
| position | with regard to 'at' can be either 'before' or 'after' | after |
| origin | XPath pointing to nodes to be inserted into referenced nodeset |
| keepValues | marker attribute. When present will keep text-values of origin nodes |

## Events

| Name | Description |
|------|-------------|
| insert | dispatched when nodes have been inserted |
| | detail[insertedNodes] - the inserted nodes |
| | detail[position] - the position of the insert in the nodeset | 

## Examples

* [Insert into inhomogenious nodeset]({{% siteparam "demoUrl" %}}insert-inhomogenious.html)
* [insert action]({{% siteparam "demoUrl" %}}insert.html)
* [insert action 2]({{% siteparam "demoUrl" %}}insert2.html)
* [TEI header editor sample]({{% siteparam "demoUrl" %}}simple-tei-header.html)
* [todo]({{% siteparam "demoUrl" %}}todo2.html)
* [the while attribute]({{% siteparam "demoUrl" %}}while.html)



