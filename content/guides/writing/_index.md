---
title: "Writing"
menuTitle: ""
date: 2024-08-01T10:29:09+02:00
tags: []
---

# General tips for authoring Fore pages

This article presents some tips to organize your Fore markup in order to ease navigating
and maintaining Fore markup.

If your use case is very simple - like a feedback form or a guestbook entry - you should probably stop here
and ask yourself if plain HTML couldn't do the job already and if there's a need for a framework like Fore altogether.

But when it comes to a bit more complex use cases and you've decided to give Fore a go, here are some 
authoring tips that hopefully help to keep your pages organized and maintainable.

## Page structure

The overall structure is like this:
- fx-fore
-- fx-model
--- fx-instance
--- fx-bind
--- fx-submission
--- fx-function
-- [UI elements] 

Though the sequence of model elements (instance, bind etc.) is not defined for authoring purposes it is
recommended to:

### keep fx-instance, fx-bind and fx-submission grouped 

Example:
```
<fx-instance id="default">
...
<fx-bind ref="instance('default')">
...
<fx-submission ref="instance('default')">
...

<!-- onward with next instance, bind and submission elements -->
```

### use prefixed ids 

It can help to keep overview by using prefixes for certain elements which makes them easier to memorize
and avoid confusion by duplicated naming.

Example:
```
<fx-instance id="i-default">
...
<fx-submission id="s-store">
...
```

### Put initialization actions to the top

It recommended to put actions reacting to 'ready' or 'model-construct-done' near the top.

Example:
```
<fx-fore>
    <fx-message action="ready">We're readyy</fx-message>
    
    <fx-model event="model-construct-done">
        <fx-message>our model is constructed - all data are loaded</fx-message>
```


