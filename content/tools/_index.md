---
title : "Tools"
date : 2020-12-11T10:42:31+01:00
chapter : true
isHome : true
tags: ["Version 1.5.x", tools, glass]
---

# Tools

> Fore Glass is not yet released but available from 'dev' branch on Github.'


With Fore you can build quite complex pages, with other pages acting as 
controls, dynamically loaded content and data and more. However with power comes 
responsibility and things can get hard to debug without good tooling.

## Fore Glass

![Fore Glass](/images/fore-glass.png)

'Fore Glass' allows to:

* log Action and Event flow - the panel on the left
* inspect the DOM tree of the page including highlighting for Fore elements - the center panel
* inspecting the state of all data sources used by the respective Fore element - the right panel
* inspect a specific control (Ctrl + i) and jump to its source element in the DOM and if bound to the bound data node
* clear Log with Ctrl+d
* configure the events you want to log


### Using Fore Glass

There are two ways to use it:

* include a `<fx-devtools>` element in your page ideally directly as a child of the `body` element. 
* or even simpler - just append the parameter 'inspect' to the URL of the page, which will inject the element for you.

## Functionality explained

Everything that happens in a Fore page is the result of some events firing. Therefore it is essential to understand, where and when
certain events fire. These are the hooks that can be used to attach the wanted behavior.

Usually - and by default - the Log panel will only show Actions that got actually triggered by an event. The action
name occurs on the left and the event name on the right.

![Fore Glass](/images/log.png)

The center panel shows the DOM tree of the Fore markup with highlighting the Fore elements. When a bound control the the DOM 
tree is clicked it will reveal it's attributes in the smaller panel and also jump to the bound data node in the right-hand panel.

![Fore Glass](/images/dom.png)

## Event logging configuration

By default the Log will only show events that actually trigger an action which is usually what you want. The event
configuration panel show you all available events at once along with a short description when you hover them.

![Fore Glass](/images/fore-glass-config.png)

To discover which events you have at hand or in which sequence they happen at which time, you can check/uncheck the intereting events
to display them in the Log.




For this example the 'model-construct', 'model-construct-done' and 'ready' have been checked, 

![Fore Glass](/images/logging.png)

> Please note the rendering of the items - events that do not have actions attached to them will occur with rounded corners.
> Actions that are executed as one block with a single update-cycle will be marked with a blue border on the left.







