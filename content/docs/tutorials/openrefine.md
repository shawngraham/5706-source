---
title: "Clearning and tidying with OpenRefine"
description: "OpenRefine is a platform run in your browser that lets you clean your data with some advanced tools."
lead: "80 to 90 percent of the time spent on any digital history project is time spent cleaning things up. OpenRefine can help."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 835
toc: true
---

In the [regex tutorial](/docs/tutorials/regex) we worked with the correspondence of the [Republic of Texas](https://en.wikipedia.org/wiki/Republic_of_Texas), and independent state from 1835 to 1846 was collated into a single volume and published with a helpful index in 1911. It was scanned and OCR'd by Google, and is now available as a text file from the Internet Archive. You can see the OCR'd text at [archive.org](http://archive.org/stream/diplomaticcorre33statgoog/diplomaticcorre33statgoog_djvu.txt).

As you worked through the regex exercise, you might have noticed that some names appear multiple times. You may also have noticed that many of the names suffered from errors in the text scan (OCR or Optical Character Recognition errors), rendering some identical names in the original document as similar, but not the same, in the file. For example the recipient "Juan de Dios Cafiedo" is occasionally listed as "Juan de Dios CaAedo". Any subsequent analysis will need these errors to be cleared up, and OpenRefine is a tool that will help us fix them.

In this exercise, we are going to use the Open Refine tool that originated with Google. Since 2012, it has been open source and freely available online. Using it takes a bit of getting used to, however.

### Installation

Start by doing the following:

1. Visit the [Open Refine home page](http://openrefine.org/) and watch the three videos.
2. Download [Open Refine 3.3](http://openrefine.org/download.html) to your machine.
3. Follow the installation instructions.
4. Start Open Refine by double clicking on its icon. This will open a new browser window, pointing to [http://127.0.0.1:3333](http://127.0.0.1:3333) or [http://localhost:3333](http://localhost:3333). This location is your own computer, so even though it looks like it???s running on the internet, it isn???t. The 3333 is a ???port???, meaning that Open Refine is running much like a server, serving up a webpage via that port to the browser. (If the browser window doesn't open automatically, open one and put [http://127.0.0.1:3333](http://127.0.0.1:3333) or [http://localhost:3333](http://localhost:3333) in the address bar.)

### Cleaning and reconciling names

1. Make sure Open Refine is running in your browser.
2. Start a new project by clicking on the ???Create project??? tab on the left side of the screen.
3. Click on ???Choose files??? and select the Texan correspondence CSV file. Open Refine will load this data and it will give you a preview of your data.
4. Name your project in the box on the top right side (eg. 'texasnames' or similar) and then click ???Create project???. It may take a few minutes.
5. Once your project has started, one of the columns that should be visible in your data is "Sender". Click on the arrow to the left of "Sender" in OpenRefine and select Facet -> Text Facet. Do the same with the arrow next to "Recipient".
6. A box will appear on the left side of the browser showing all 189 names listed as senders in the spreadsheet.  Within the "Sender" facet box on the left side, click on the button labeled "Cluster". This feature presents various automatic ways of merging values that appear to be the same.
7. Play with the values in the drop-down boxes and notice how the number of clusters found change depending on which method is used. Because the methods are slightly different, each will present different matches that may or may not be useful.
8. If you see two values which look like they should be merged, e.g. `Ashbel Smith` and `. Ashbel Smith`, check the box to the right in the 'Merge' column and click the 'Merge Selected & Re-Cluster' button below.
9. Go through the various cluster methods one-at-a-time, including changing number values, and merge the values which appear to be the same. `Juan de Dios CaAedo` clearly should be merged with `Juan de Dios Cafiedo`, however `Correspondent in Tampico` probably should not be merged with `Correspondent at Vera Cruz`. Since we are not experts, we will have to use our best judgement in these cases ??? or get cracking on some more research to help us make the call. By the end, you should have reduced the number of unique Senders from 189 to around 150.
10. Repeat these steps with Recipients, reducing unique Recipients from 192 to about 160.
11. To finish the automatic cleaning of the data, click the arrow next to "Sender" and select 'Edit Cells -> Common transforms -> Trim leading and trailing whitespace'.
Repeat step 12 for "Recipient". The resulting spreadsheet will not be perfect, but it will be much easier to clean by hand than it would have been before taking this step.
Click on ???Export??? at the top right of the window to get your data back out as a .csv file.

Ta da! A file ready for some network analysis. Stash a copy of your cleaned correspondence network csv file in your repo.
