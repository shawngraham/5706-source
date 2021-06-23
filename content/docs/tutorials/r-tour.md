---
title: "A Quick Tour of RStudio"
description: "The RStudio Interface"
lead: "This page is a supplement to any of the R based tutorials."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 748
toc: true
---

_By Chantal Brousseau_

# Working with R

R is a programming language designed for statistical computing and graphics creation, so it is *excellent* when it comes to analyzing large sets of data and creating visualisations from it-- which tends to be a big part of our work in digital humanities! The language was designed by and for statisticians and data analysts, thus many of those with little or no experience with programming find R a bit easier to understand and use than other programming languages. In this class, you can choose to use Python, R, or both! It's just a matter of figuring out what works best for you.

R and R Studio can be installed through the Anaconda Navigator by hitting the 'install' button on their 'card' in the initial interface.

However, just for your information: you can install it directly after you've [downloaded it here](https://rstudio.com/products/rstudio/download/#download) (we want the desktop version). RStudio is an integrated development environment (IDE) for R, which means it lets you do everything you can with R all from one place on your computer!

**If you're installing R Studio directly, you also need to get R [at this link](https://cran.r-project.org/) to go to the CRAN (Comprehensive R Archive Network) home page, then choose your OS to be taken to the appropriate R download for your machine.**



## Working in RStudio

So you have everything installed, you launch RStudio on your computer, and you see this:

![](/images/rstudio/rs1.png)

Kind of intimidating, maybe, so let's take a more detailed look at all the parts you'll need to know. To write a program in R, you need to create a new R Project, which can be done by:

1) Going to the upper right corner of RStudio where it says `Project: (None)`
2) Selecting "New Project", then:
    a. `New Directory` if you don't already have a folder created with some data you want to analyze in it.
    b. `Existing Directory` if you already have a folder on your computer you want to work in aka a folder with the data you want to analyze.

![](/images/rstudio/rs2.png)

You'll then want an `R Script`-- a place where you can actually write code! This can be done by selecting `File` from the top menu bar, then going down to `New File` and finally selecting the `R Script` option.

![](/images/rstudio/rs3.png)

Now that you've done that and you (*should*) have an extra pane, shall we go on a little tour?

![](/images/rstudio/rs4.png)

### Optional

It might still seem a bit confusing, and that's okay, because this is all brand new for you! My challenge to you is to first get yourself a bit more familiar with R as a language by following along with [this notebook](https://mybinder.org/v2/gh/ChantalMB/cleaning-data-r/master).

Once you've done that:
1) Download the data from that [tutorial's repository](https://github.com/ChantalMB/cleaning-data-r/tree/master/data) and place it in a new folder on your computer.
2) In RStudio, create a new project using the `Existing Directory` option, setting the working directory as the folder you just created.
3) In a new R script, re-do the tutorial but this time just use the notebook as a guide and do each step in RStudio instead!
