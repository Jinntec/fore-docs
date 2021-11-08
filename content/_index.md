+++
title = "Frequently Asked Questions"
date = 2020-12-11T10:42:31+01:00
chapter = false
weight = 2
isHome = true
+++

# Tuttle Documentation

This is the documentation site for 'Tuttle - a eXist-db Git integration'

This website contains: 
* Get started
* Frequently Asked Questions

## How to contribute to this FAQ

### Proposing new entries

If you'd like to propose an entry not having it all prepared yet, please consider creating a ticket in the issue tracker. You can suggest a topic, solicit opinions and also subsequently collaborate and discuss the shape of the corresponding article in there.

The website is directly generated from the markdown files stored in the `content` subdirectory of the [github repository](https://github.com/eeditiones/tuttle-doc/tree/main/content). All contributions are welcome.

### Quick edits via GitHub

You can make changes to any existing page by clicking on the **Edit this page** link at the top right of the page. All you need is a GitHub user account. Clicking the link will open the corresponding markdown file on github for editing and you can start applying your changes immediately.

To add new files, navigate to the correct subdirectory in the [github repository](https://github.com/eeditiones/tuttle-doc/tree/main/content) and press the **Add file** button on the top right above the directory listing. Files should be markdown, i.e. the file name must end with `.md`.

Once you are done with editing, fill out the **Propose changes** form at the bottom of the page and click the green button. Changes will not go live immediately. Instead, you are asked to create a so called *pull request*, which will then be reviewed by a core team member. You do not need to fill out anything if you already provided a description of your changes, so just press the green **Create pull request** button (also on the followup page).

To work on larger, new articles we recommend to write your text offline first in an editor of your choice. Most text editors (including oXygen) provide some support for writing markdown. You can then upload your new file using **Add files** (see above).

### Forking the repo

To work on more than just one article at a time, it is better to fork the [faq repository](https://github.com/eeditiones/tuttle-doc) and clone it to your local machine. Once you're done, commit the changes to your fork and open a *pull request* on the source repository.

To preview your changes locally, you need to install a software package called [hugo](https://gohugo.io/getting-started/installing). Next, clone the repository to your local machine, cd into it and run the following command once to load the require theme for the FAQ:

```sh
git submodule update --init --recursive
```

You may then start a local hugo server with

```sh
hugo server
```