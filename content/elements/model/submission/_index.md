---
title: "<fx-submission>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, model, submission]
---

## Description

Send and receive data.


## Attributes
| Name | Description | Default |
|------|-------------| -------- |
| ***id*** | id of submission for referral |  |
| ***ref*** | XPath reference pointing to the bound node |  |
| instance | id of instance when `replace='instance'` |  |
| into | XPath expr where to insert response nodes into |  |
| method | http methods GET, POST, PUT, DELETE, url-encoded-post | GET  |
| nonrelevant | handling of non relevant nodes during serialization. Can be one of 'keep', 'empty' or 'remove' | remove  |
| replace | one of 'all', 'instance', 'target', 'redirect' or 'none' | all  |
|  | 'all' - response replaces the viewport |   |
|  | 'instance' - response replaces the instance given by the `instance` attribute or if not present the default instance |   |
|  | 'target' - response will be attached to element identified by `target`| |
|  | 'redirect' - use response as redirect url. | |
|  | 'none' - response will be ignored. | |
| serialization | 'none' or 'xml' at this point | xml |
| targetref | XPath pointing to target node when `replace="instance" | |

## Events
| Name | Description | 
|------|-------------| 
| submit | dispatch before submission takes place |
| submit-error | dispatched if the request returned an error |
| submit-done | dispatched when submission was successfully completed |


## Examples

* [auth]({{% siteparam "demoUrl" %}}auth.html)
* [submission relevance]({{% siteparam "demoUrl" %}}submission-relevance.html)
* [submission serialization]({{% siteparam "demoUrl" %}}submission-serialize.html)
* [submission serialization]({{% siteparam "demoUrl" %}}submission-serialize.html)
* [submission demo]({{% siteparam "demoUrl" %}}submission1.html)
* [submission demo2]({{% siteparam "demoUrl" %}}submission2.html)
* [submission chaining]({{% siteparam "demoUrl" %}}submission3.html)
* [submission chaining]({{% siteparam "demoUrl" %}}submission4.html)
* [submission with targetref]({{% siteparam "demoUrl" %}}targetref.html)



