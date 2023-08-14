---
title: "<fx-insert>"
date: 2021-12-14T17:41:11+01:00
tags: [elements actions]
weight: 60
---

## Description

Action to insert node(s) into instance data.

## Attributes

| Name | Description | Default |
|------|-------------| --------|
| at | index position in nodeset where to insert new node(s) | 0 |
| context | optional XPath pointing to parent node of node to insert | |
| position | with regard to 'at' can be either 'before' or 'after' | after |
| origin | XPath pointing to nodes to be inserted into referenced nodeset | |
| keepValues | Boolean attribute. When present will keep text-values of origin nodes | false |
| ref | XPath pointing to node(s) to insert. If `context` is given `ref` is relative to that | |


## Events

| Name | Description |
|------|-------------|
| insert | dispatched when nodes have been inserted |
| | detail[insertedNodes] - the inserted nodes |
| | detail[position] - the position of the insert in the nodeset | 

## Examples

* [Insert into inhomogenious nodeset]({{% siteparam "demoUrl" %}}insert-inhomogenious.html)
* [insert action]({{% siteparam "demoUrl" %}}insert.html)
* [insert with context]({{% siteparam "demoUrl" %}}insert2.html)
* [TEI header editor sample]({{% siteparam "demoUrl" %}}simple-tei-header.html)
* [todo]({{% siteparam "demoUrl" %}}todo2.html)
* [the while attribute]({{% siteparam "demoUrl" %}}while.html)



