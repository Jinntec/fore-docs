---
title: "Writing Fore pages"
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
* fx-fore
  * fx-model
    * fx-instance
    * fx-bind
    * fx-submission
    * fx-function
  * [UI elements] 

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

This eases to find/navigate constraints as well as
submissions that belong to certain data.

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

Naming is an art but prefixing can help - often a name like 'person' would
apply nicely to the data as well as in other places. By just 'adding' an 'i-' (for instance) to
fx-instance ids helps to get the right context and is easy to remember.

Conventions we use:
* rather no prefix for instance id (considering those as the entity we deal with)
* 's-' for submission ids
* 'r-' for repeat ids
* 'c-' for case ids

It doesn't matter but choosing a pattern and sticking to it
helps a lot to avoid problems.


### Put initialization actions to the top

It recommended to put actions reacting to 'ready' or 'model-construct-done' near the top.

Example:
```
<fx-fore>
    <fx-message action="ready">We're readyy</fx-message>
    
    <fx-model event="model-construct-done">
        <fx-message>our model is constructed - all data are loaded</fx-message>
```

When reading the form these will the entry points to the page and
therefore should be kept near the top.

## Put document-level actions to the top

Likewise with actions that attach to the `document` or `window` object. 

These should be placed as direct childs of `<fx-fore>` due to their 
global scope. 
