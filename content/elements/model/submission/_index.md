---
title: "<fx-submission>"
date: 2021-12-14T17:41:11+01:00
tags: [elements, model, fx-submission]
---

## Description

Send and receive data.


## Attributes
| Name | Description | Default |
|------|-------------| -------- |
| credentials | sets credentials policy - one of 'omit', 'same-origin' or 'include' | same-origin |
| id | required: id of submission for referral | 'default' |
| ref | XPath reference pointing to the bound node | root node of default instance |
| instance | id of instance when `replace='instance'`. Required when replace='instance' |  |
| into | XPath expr where to insert response nodes into |  |
| method | http methods GET, POST, PUT, DELETE, url-encoded-post | GET  |
| nonrelevant | handling of non relevant nodes during serialization. Can be one of 'keep', 'empty' or 'remove' | remove  |
| replace | one of 'all', 'download', 'instance', 'target', 'redirect' or 'none' | all  |
|  | 'all' - response replaces the viewport |   |
|  | 'download' - save dialog is shown for response | |
|  | 'instance' - response replaces the instance given by the `instance` attribute or if not present the default instance |   |
|  | 'target' - response will be attached to element identified by `target` (CSS Selector syntax e.g. '#mydiv')| |
|  | 'redirect' - use response as redirect url. | |
|  | 'none' - response will be ignored. | |
| serialization | 'none' or 'xml' at this point | xml |
| target | selector in CSS selector syntax. valid only when replace is 'target'.  | |
| targetref | XPath pointing to target node when `replace="instance"` | |
| validate | Boolean to turn validator mode on/off | true |

 
## Events
| Name | Description | 
|------|-------------| 
| submit | dispatch before submission takes place |
| submit-error | dispatched if the request returned an error |
| submit-done | dispatched when submission was successfully completed |


## URL Schemes

Beside http, https Fore supports:

  * 'localStore:[key]' to manage data in the browsers' localstorage (supports 'get', 'post', 'delete' and 'consume' methods
  * '#echo' to echo back whatever got sent 
  
## Examples

* [auth]({{% siteparam "demoUrl" %}}auth.html)
* [submission localStore]({{% siteparam "demoUrl" %}}submission-localStore.html)
* [submission serialization]({{% siteparam "demoUrl" %}}submission-serialize.html)
* [submission demo]({{% siteparam "demoUrl" %}}submission1.html)
* [submission demo2]({{% siteparam "demoUrl" %}}submission2.html)
* [submission chaining]({{% siteparam "demoUrl" %}}submission3.html)
* [submission chaining]({{% siteparam "demoUrl" %}}submission4.html)
* [submission with targetref]({{% siteparam "demoUrl" %}}targetref.html)
* [handling credentials]({{% siteparam "demoUrl" %}}submission-credentials.html)



