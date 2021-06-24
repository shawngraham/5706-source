---
title: "Static Websites"
description: "Control your own narrative"
lead: "Static websites are not driven by a database; they are more secure and more likely to last into the future."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 780
toc: true
---

Building a website from scratch can be onerous. Using a system like Wordpress or Squarespace etc can leave you locked in to someone else's platform (and any security issues that might entail).

Here, we're going to build a simple website that uses nothing but text files as its source; these text files will always be readable into the future, and you can also copy them to your own machine so that they're always handy, ready to be transformed into something else.

I'm talking about _static site building_; there are many different generators out there that will take your text files, pump them through some templates, and spit out flat html on the other side. At The Programming Historian, there is a lesson by Amanda Visconti on using [Jekyll and Github Pages](https://programminghistorian.org/en/lessons/building-static-sites-with-jekyll-github-pages) to make a site; we're going to do something much easier.

In essence, you are going to create a new repository in your Github account called `your-username.github.io`; you're going to make a file in there called `index.md` and you're going to write something in that file, eg,

```
## My Quick Static Site

This is a site I build with gh-pages. **Wow**

It reads [markdown](https://www.markdownguide.org/) and turns it into html.

![gif ftw](https://media.giphy.com/media/nXxOjZrbnbRxS/200w_d.gif)
```

Commit that file. Then, hit the gear wheel icon and scroll down to the Github Pages section. Enable Github Pages. Github will run your text files through the Jekyll site builder for you; here you can select from some of their templates. It will tell you where your site can be found: ie `https://your-username.github.io`. If you created a file `about.md` in that repo, it would be at `https://your-username.github.io/about`.

Boom! [The full process is on this site with screenshots](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site).

Now, there's a lot more to static websites than this. This course site is generated with [Hugo](https://gohugo.io); a site generator for building exhibitions, called 'Wax', is available [here](https://minicomp.github.io/wax/). (Speaking of exhibits, here's information about building them with [Omeka.net](https://programminghistorian.org/en/lessons/up-and-running-with-omeka).)

(A word about Hugo: any [theme](https://themes.gohugo.io/) that you download to use with Hugo will contain within it a folder called 'ExampleSite'. The easiest way to get going is to copy the contents of the example site folder to your the 'quickstart' folder you create as part of the [create new site](https://gohugo.io/getting-started/quick-start/) process, in liu of step four, and then overwrite the demo content. Once you've got the content the way you want it, build the site with the `hugo` command; the site will be in the `public` folder. Drag and drop all of the content inside this folder into a new github repository. Enable github pages, make sure the source for github pages is set to the `main` branch, and you'll be good to go!)


Customize your new site to be a 'front page' for your experience in this course; when you build your own digital history project, you could add your devlogs as pages to this site.
