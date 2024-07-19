---
title: "Scopes"
menuTitle: ""
date: 2024-07-19T10:19:53+02:00
tags: [Guides]
---

![Scopes](/images/scope1.svg)

Each `<fx-fore>` element creates its own scope which controls:
* access to data
* evaluation of bindings
* evaluation of ids
* events

For the above graphic that means that data, ids and bindings being used in the inner Fore are being resolved within
its boundaries and events won't propagate upwards to the outer Fore.

Likewise the outer Fore has no direct access to the inner Fore (unless using the API within a custom function). 

## Fore scopes versus shadowDOM

Some background for the Web Components-savy:
the content you put into a Fore element is not encapsulated in a shadowDOM but visible within 
the light or global DOM and therefore be styled without any restrictions with CSS.

Using shadowDOM for style encapsulation is of less importance with the advent of nested CSS which
makes it easy to achieve style-scoping. Otherwise it often creates problems with flexibility and is 
generally avoided throughout Fore.

So unlike shadowDOM Fore allows for global styling. 

However like shadowDOM Fore events are scoped to the next parent `<fx-fore>` element and are not leaving
its scope.



