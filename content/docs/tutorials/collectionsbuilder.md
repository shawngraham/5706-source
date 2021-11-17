---
title: "Online Exhibits and Colletions"
description: "You could build one from scratch. But this is a lot easier."
lead: "There are a variety of tools out there to help you; here's a walkthrough with one of the newer ones."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 782
toc: true
---

There are a number of ways to get cultural heritage materials online so that they can be reused, explored, or enjoyed by others, ranging from the database-driven [Omeka.org](https://omeka.org) and the hosted version [Omeka.net](https://omeka.net) to frameworks such as [Wax](https://minicomp.github.io/wax).

Given what we've seen about making [static websites with github](/docs/tutorials/static-websites/), this particular walk-through will explore how to get [CollectionBuilder](https://collectionbuilder.github.io/) up and running via Github.

## Collectionbuilder

CollectionBuilder, from the [University of Idaho Library](https://www.lib.uidaho.edu/) is a series of Jekyll-powered templates that take metadata about your collection, arranged in a csv file, and produces a website to display your digital collection. It comes with maps, data download, search and more.

Currently, there are three separate templates one could use. [The first uses Github Pages](https://collectionbuilder.github.io/gh/) to power the complete website _including_ storage of your collection objects (pictures, videos, etc). [A demo of this template is behind this link.](https://collectionbuilder.github.io/collectionbuilder-gh/)

The second template, [CollectionBuilder-CSV](https://collectionbuilder.github.io/csv/) allows for greater customization, and you can use it with assets that are elsewhere - perhaps a local historical society has already uploaded a number of photographs to Flickr for instance, and wants to do something more involved. [There is a demo of this template behind this link](https://www.lib.uidaho.edu/queered/).

The third template is for using with the 'ContentDM' service; it applies a 'skin' overtop an existing collection served up by ContentDM. We won't be using or exploring ContentDM. You can find out more about the third template [here](https://collectionbuilder.github.io/cdm/) if you want, and more about [ContentDM here](https://www.oclc.org/en/contentdm.html).

## Collectionbuilder-GH

CollectionBuilder is well supported with documentation and tutorials. The GH-Pages powered template (meant for small collections, where everything - including the cultural heritage materials - are held in the same repository) [is available here](https://github.com/CollectionBuilder/collectionbuilder-gh). I am going to direct you here to their [workshop materials for this template](https://collectionbuilder.github.io/workshop/gh/) and suggest you work through those.

[Here is the template itself](https://github.com/CollectionBuilder/collectionbuilder-gh).

1. To get started, log into Github. Then, go to this repo and click on the green 'Use this template' button.
2. Go to the repo settings for the repo you created when you clicked on that button. Turn on the GH Pages option. This will trigger Github to use Jekyll to turn the template into a site. You'll find the location of your site **a few minutes later** at `https://your-username.github.io/name-of-repo`.
3. Now, back in your repository, there is a file at its top level called `_config.yml`. Go to that file; it's at `github.com/your-username/whatever-you-called-the-repo/blob/main/_config.yml`. Hit the edit icon (looks like a pencil). This file lists a bunch of settings. You'll want to change line 12 to remove the `#` to set the `url:` variable to point to your live site, eg, something like: `url: https://your-user-name.github.io`. Line 14 you'll give the name of the repo: `baseurl: name-of-repo`. Further down, at lines 23, 25, 28 and 30 are settings for the site title, tagline, description, and author. **NB** If you put a colon anywhere in the values in a yml file, you will break your website. So if you wanted the site title to be something like `HIST5706: Embrace the DH`, you'd change line 23 like this: `title: "HIST5706: Embrace the DH"`. That is, you _wrap_ the text in quotation marks, so that the machine knows that the colon isn't trying to define a variable setting.

<iframe width="560" height="315" src="https://www.youtube.com/embed/FbWGLFRpAlA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

4. Now you have a site. Congratulations! But it's got nothing in it. [At this point, I'm going to just hand off to the existing tutorial here](https://collectionbuilder.github.io/workshop/gh/prepare.html). Follow along with that, it's great!

If you want to use your _own_ materials, rather than the ones used in the Workshop, collect the images/pdfs into a folder on your machine. **No spaces in filenames!!!** Then, use this [Collectionbuilder-gh google sheet](https://docs.google.com/spreadsheets/d/1Uv9ytll0hysMOH1j-VL1lZx6PWvc1zf3L35sK_4IuzI/edit#gid=0) to organize your metadata. (Here is the [documentation about how the metadata should be formatted](https://collectionbuilder.github.io/cb-docs/docs/metadata/gh_metadata/)). Take a copy of that sheet, then fill it out appropriately for your materials. Save it as csv to your machine. Let's assume you've called the file `my-metadata.csv`.

You'll then load your objects that you collected into the `objects` folder in your repository.

Upload your `my-metadata.csv` to the `_data` folder. **THEN** go back to the `_config.yml` file, hit the 'edit' button, and change line 37 to point to _your_ metadata **without** the .csv: `metadata: my-metadata`

Once you make this final change (hitting the commit button), the site will build and will be populated with _your_ materials.

There - _that_ was easy! [You can explore the rest of the workshop to see how to customize more of the site.](https://collectionbuilder.github.io/workshop/gh/). (Incidentally, this workshop was for DH2020 which, sigh, was _supposed_ to happen in Ottawa.)

## Collectionbuilder-CSV

The same process will get you started with Collectionbuilder-CSV, but there are some tricksy bits that I will explain.

As with the GH pages version, you [go to the repository and click the green 'use this template' button](https://github.com/CollectionBuilder/collectionbuilder-csv). You'll do the same process again.

Here's the [metadata google sheet to use](https://docs.google.com/spreadsheets/d/1nN_k4JQB4LJraIzns7WcM3OXK-xxGMQhW1shMssflNM/edit?usp=sharing), take a copy, fill it out, save to your own machine as `my-metadata.csv` once you've filled it out; note that _now_ we're pointing to files available on the web for our objects. You could go to [unsplash.com](https://unsplash.com) and find photos to test with; right-click on the image to get the direct URL. Then you put that URL in the appropriate spot in the csv file.

Update the `_config.yml` file the same way as before. Here's an excerpt from my config:

```
# site domain, full URL to the production location of your collection
url: https://shawngraham.github.io
# path to location on the domain if necessary e.g. /digital/hjccc
baseurl: /test-collectionbuilder
# location of code, the full url to your github repository
source-code: https://github.com/shawngraham/test-collectionbuilder

<snip!>

metadata: demo-sg

```

### Now the tricksy bit

When you made all of those changes ('commits', remember), you triggered Github to try to run its default Jekyll engine on the code. **This will not work**. Instead, we're going to give Github some special instructions - called 'actions' - to get Github to do things the way we want (full documentation of this step is [here](https://collectionbuilder.github.io/cb-docs/docs/deploy/actions/)).

Back on the home page for your repository, you're going to create a special file. Click "add file > create new file". Type in the following exactly as the file name:
 `.github/workflows/jekyll.yml`

 **and yes that is a period in front of the word github!** Then, in the editor window, paste the following:

```
name: build site with jekyll and deploy on github pages

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  jekyll:
    runs-on: ubuntu-18.04 # ubuntu-latest is now 20.04 and doesn't seem to work
    steps:
      # checkout code
      - uses: actions/checkout@v2

      # Use ruby/setup-ruby to shorten build times
      # https://github.com/ruby/setup-ruby
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: 2.7 # Not needed with a .ruby-version file
          bundler-cache: true # runs 'bundle install' and caches installed gems automatically

      # use jekyll-action-ts to build
      # https://github.com/limjh16/jekyll-action-ts
      - uses: limjh16/jekyll-action-ts@v2
        with:
          enable_cache: true

      # use actions-gh-pages to deploy
      # https://github.com/peaceiris/actions-gh-pages
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          # GITHUB_TOKEN secret is set up automatically
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_site
```

Hit the green commit button.

## One last thing

Now, go to your repo settings, select 'Pages', and change the branch from `main` (or possibly, 'master') to `gh-pages`.

In a few minutes, your site should be up and running at `https://your-user-name/github.io/name-of-repo`.

### A few customizations

If you'd like to change the site logo, you can put the complete URL to a graphic in your `_config.yml` document at line 34 & 35, eg:

```
organization-link: https:/electricarchaeology.ca/
organization-logo-banner: https://graddh.netlify.app/images/dhcu-logo.png
organization-logo-nav: https://graddh.netlify.app/images/dhcu-logo-small.png
```

You can change the main site image by going to `_data/theme.yml` and changing the `featured-image:` variable, eg:

```
# featured image is used in home page banner and in meta markup to represent the collection
# use either an objectid (from an item in this collect), a relative location of an image in this repo, or a full url to an image elsewhere
featured-image: https://electricarchaeologist.files.wordpress.com/2021/08/laocoon.jpg
```

A thing about the featured-image: setting. You could set it to an object in your metadata, eg `featured_image: demo_008` where 'demo_008' was the identifier of a row of data in that metadata file. **But if you made a mistake here, say you typed `demo_08` then, since that object does not exist, your build will break! So make sure you've got things pointing to objects that actually exist.

You can play with the map settings - including the basemap, in the same file from about line 38 further. Indeed, there's a lot you can set in this theme.yml file, so give it a whirl! Line 81 is interesting; it loads up default themes from [bootswatch.com](https://bootswatch.com). Go to that site, check out which ones seem fun, and then change line 81 to use the theme you like. I kinda like 'sketchy', myself.
