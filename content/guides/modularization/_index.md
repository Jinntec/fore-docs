---
title: "Modularization"
menuTitle: "Modularization"
date: 2023-07-26T10:53:29+02:00
tags: [guides]
---

![Modularization](/images/tangram.png)

> "Modularization is the activity of dividing a product or system into interchangeable modules." (stolen somewhere)

As long as things stay simple and you have just a bunch of controls, there's not much logic and just a few data fields
you don't have to worry much about Modularization.

However, if you're building a whole application things will quickly change - the markup grows and grows with some
undesired effects on productivity:
* a large file is less readable and maintainable
* merge conflicts may arise more often when working with several developers on the same thing
* you probably would need to repeat yourself just to have a block of related content in different places
* scrolling up and down can become a nightmare just to see where certain idrefs point to

## Modularization with Fore

Luckily Fore has several ways of dealing with this. You don't need a detailed plan upfront, but can use one of the features
below to modularize when time has come. 

### Including an external [ForeBody](/glossary/#forebody)

Starting with the easiest method of factoring out a block of markup and loading it from an external file:


 
```
<fx-fore src="hello.html"></fx-fore>
```

When the browser hits the `fx-fore` element it will first look for a `src` attribute and if present, load the external page.

The page is searched for the first `fx-fore` element which gets extracted and replaces the original `fx-fore` element.

> Please note that this approach allows to develop a standalone page and make it work individually and later use
> the unmodified page included in some other page. WARNING: please be aware that the CSS of the loaded page is not imported
> as just the `fx-fore` element is extracted. That could be a future enhancement.

As a consequence the import of the external file is always happening and cannot be cancelled or (directly) reverted. Using
`<fx-fore src="mypage.html">` can be thought of as a simple include. It's fine to break down larger pages into 
smaller units but does not offer support for reducing the page load.

#### passing attributes and classes to the imported page

All attributes and CSS classes given to a `fx-fore` element will be passed down to the replacing element.

For easy access to these attributes from within the loaded page there is the `fore-attr()` function.

```
<fx-fore src="hello1.html" class="myClass" attr1="world"></fx-fore
```

Fore element in html1.html:
```
<fx-fore>
    Hello {fore-attr('attr1')}
</fx-fore>
```

If you inspect the live demo with devtools you'll see that `myClass` and `attr1` are preserved. 

> You'll see an additional attr 'from-src' which contains the value of the original `src` attribute. This is not
> of significance for now but might get used in the future.

<fx-fore src="hello1.html" class="myClass" attr1="world"></fx-fore


<fx-fore class="myClass"></fx-fore>

### Fore as control

A `fx-fore` element can be used as a control like this:
```
<fx-fore>
    ...
    <fx-control ref="item" url="myForeControl.html">
        <label>A nested Fore acting as control</label>
    </fx-control>
    ...
</fx-fore>
```

At runtime this will be expanded to this:
```
<fx-fore>
    ...
    <fx-control ref="item" url= "myForeControl.html">
        <label>A nested Fore acting as control</label>
        <fx-fore class="widget">
            <!-- content of myForeControl.html -->
        </fx-fore>.
    </fx-control>
    ...
</fx-fore>
```

There are no restrictions regarding the complexity or size of the embedded [ForeBody](http://localhost:1313/fore-docs/glossary/#forebody).

> for Web Components experts: Fore lives by default in the lightDOM but still restricts its events to the respective
> scope of a `fx-fore` element. Styling therefore can be applied globally.

#### Passing data to the Fore widget

To be useful there needs to be a way to pass in initial data for the embedded Fore. This is accomplished with the `initial`
attribute.
 
```
    <fx-control ref="item" url="myForeControl.html" initial=".">
        <label>A nested Fore acting as control</label>
    </fx-control>
```

`initial` is an XPath expression that resolves relative to the `ref` node. Here (wich is a common case) we just pass
in the node that we are binding to in our outer [ForeBody](http://localhost:1313/fore-docs/glossary/#forebody).

After the Fore control has initialized it will get the following default instance.

```
<fx-instance>
    <data>
        <item>[value of bound node in outer ForeBody]</item>
    </data>
</fx-instance>
```

The embedded [ForeBody](http://localhost:1313/fore-docs/glossary/#forebody) can now work with this data as usual.

#### Returning data to outer ForeBody

When an `fx-control` embeds a [ForeBody](http://localhost:1313/fore-docs/glossary/#forebody) it will start listening
for a `return` event.

Whenever the embedded [ForeBody](http://localhost:1313/fore-docs/glossary/#forebody) decides to be done (on `value-changed` in example below) it will fire
the `return` event passing back the resulting data in the `nodeset` property. The control will use that and mount
the data to its binding. Let's assume the user typed 'result':

```
<fx-fore>
    <fx-model>
        <fx-instance>
            <data>
                <item>result</item>
            </data>
        </fx-instance>
    <fx-model>
    <fx-control ref="item" url="myForeControl.html" initial=".">
        <label>A nested Fore acting as control</label>
        <fx-fore>
            <fx-control ref="item">
                <label>Your item</label>
                <fx-return event="value-changed" ref="."></fx-return>
            </fx-control>
        </fx-fore>
    </fx-control>
```

The returned data can be element nodes, an attribute node or text nodes and replace the bound node of the control. 

This means that complete subtrees of data can be mounted back into
the outer Fore.

```
<data>
    <!-- this data do not match the above example - just for illustration -->
    <item instock="true">
        <article-number>1234</article-number>
        <name>Sneeeaakr</name>
    </item>
</data>
```

> Warning: this feature is limited to the use of HTML or XML as data model. JSON support is still limited though
> planned for the future.

Using nested Fore elements like this the most powerful technique to modularize applications into smaller functional
pieces. A 'control' can handle arbitrary complex logic within itself and only present the results back to its
outer Fore. Existing ForeBodies can be embeded within another with minimal effort and still stay independent pages that
can be developed and tested separately. 


### Load on Demand

For bigger applications you probably want to limit the pageload as this often involves optional or dynamic views
that you ideally only want 'to pay for' when really needed.

You can also just start with minimal UI and load everything dynamically.

With the `fx-load` action a lot of different scenarios can be accomplished and i'll not going into navigational features
of the load action here, as these are well documented in [the load demo]({{% siteparam "demoUrl" %}}load.html).

For modularization purposes `fx-load` offers two options:

#### Loading a template

A `fx-load` action specifying an HTML `template` element is useful if you have rather small snippet of HTML content
to insert into your UI.

As all actions `fx-load` reacts to a certain event and it depends on your use case which one to choose.

```
<fx-load attach-to="#lazyControl" id="first" event="anyEvent">
    <template>
        <fx-control ref="item">
            <label>an item:</label>
        </fx-control>
        <fx-output ref="item"></fx-output>
    </template>
</fx-load>
<div id="lazyControl"></div>
```

The template may contain any kind of HTML including of course all Fore elements.

When the event fires the `fx-load` action will clone the template and insert it into the DOM at the
position specified by `attach-to`. It expects an id given in CSS selector syntax starting with a '#'.

The content of the target element will be replaced with the cloned template content.

```
<div id="lazyControl">
    <fx-control ref="item">
        <label>an item:</label>
    </fx-control>
    <fx-output ref="item"></fx-output>
</div>
```

#### Loading external content

If bigger chunks of content shall be loaded or you like to keep the content in a separate file, you can use the 
`url` attribute.

```
<fx-fore>
    <fx-load event="ready" url="load-snippet.html" attach-to="#thetarget"></fx-load>
    <fx-message event="loaded">url {event('url')}</fx-message>
    <div id="thetarget"></div>
</fx-fore>
```

Inserting a full HTML page into another breaks the page and must be avoided. Thus, the content of the `body` is used
for insertion at `attach-to` node.

However if the loaded content contains another `fx-fore` element it is assumed that this should be loaded instead.

When content became available `fx-load` will fire a `loaded` event in case some post-import actions need to be done.
 
#### Unloading content

To unload content and remove it from DOM again, the load action can simply provide a template with an empty
HTML element.

As the content replaces the content of the target element, this will effectively remove whatever there has been before.

```
<fx-load attach-to="#lazyControl" event="anyEvent">
    <template><div></div></template>
</fx-load>
<div id="lazyControl"></div>
```


### Summary

* For simple inclusion of a [ForeBody](http://localhost:1313/fore-docs/glossary/#forebody) use `<fx-fore src="myfore.html">`
* When assembling complex data-structures `<fx-control url="myfore.html">` is helpful to break things down
* With efficiency and lazy-loading on mind you should go for `<fx-load>`

Of course these approaches can also be combined.




