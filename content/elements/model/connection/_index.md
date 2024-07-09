---
title: "<fx-connection>"
menuTitle: ""
date: 2024-06-13T16:51:42+02:00
tags: []
weight: 7
---

## Description

`fx-connection` allows to use WebSocket connections to share data between different browser windows - either locally or remote.

"messages" are snippets of data in text, json or xml format that are transferred via Websocket connections.

The `fx-connection` element allows to bind messages to data directly thereby updating local data whenever a message is received.
To send a message the [`fx-send`](/elements/actions/send) action is used as with `fx-submission`.

If no direct binding is desired the message content can also be accessed via the `event()` function.

## Attributes
| Name | Description | Default |
|------|-------------| -------- |
| heartbeat | an integer value for the duration between heartbeats | 0 |
| message-format | dataformat of message. can be 'json', 'text' or 'xml' | 'json' |
| url | the websocket url e.g. ws://localhost:8088 | - |

## Examples

* [chat]({{% siteparam "demoUrl" %}}chat.html)
