---
title: "Get Started"
menuTitle: "Get Started"
date: 2021-12-14T17:41:11+01:00
weight: 1
chapter: false
---



This tutorial will walk you through the first steps of using Fore and introduce some
of the elements.

For further study it is highly recommended to use the huge list of demos that come with Fore.
These showcase all features and how to use them in concrete working examples.

## Using Fore

To use Fore you have to add one CSS stylesheet and the Fore module to your page.
### Loading from CDN

Add these tags to the head of your HTML file.
```
<link rel="stylesheet" 
      href="https://cdn.jsdelivr.net/npm/@jinntec/fore@latest/resources/fore.css">

<script type="module" 
        src="https://cdn.jsdelivr.net/npm/@jinntec/fore@latest/dist/fore.js">
```

You are good to go and may skip to next section!

> If you are situated within the European Union you should always bundle a Fore distribution with your code to avoid conflict with
> data privacy protection regulations.

### Using local copy

Download Fore from [github](https://github.com/Jinntec/Fore/releases) and unpack it to a convenient location on your disk.

Setup a basic HTML page like this:
```
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <meta content="width=device-width, minimum-scale=1, initial-scale=1, user-scalable=yes" name="viewport"/>
    <title>template</title>
    <link href="[path-to-fore]/resources/fore.css" rel="stylesheet">
</head>
<body>
<script type="module" src="[path-to-fore]/dist/fore.js"></script>
</body>
</html>
```

'[path-to-fore]' has to be the relative path to the Fore location on your disk.

### Using NPM

`npm i --save @jinntec/fore` 


## Using the dev version

During development it can be helpful to get console messages that give some feedback about
what is happening behind the scenes. The dev version also includes additional tools to support the developer:

* `fx-inspector` which is a simple instance data viewer showing all data in a collapsible side-panel on the right. It can display XML and JSON data
* `fx-devtools` aka 'Fore Glass' which allows you to log all events and actions, inspect the DOM elements and showing a live view of all data. Fore Glass is available from version 2.0.0.  


To get those message on developers tools console just use:
```
<script type="module" src="[path-to-fore]/dist/fore-dev.js"></script>
```

Once in production you can simply switch back. There's no difference between these versions beyond 
logging.




