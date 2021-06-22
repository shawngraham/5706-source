---
title: "Text Analysis: AntConc "
description: "AntConc is a tool for exploring concordances"
lead: "AntConc is a tool for exploring concordances within a corpus of texts."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 815
toc: true
---

### Jump right in

Follow this [tutorial by Heather Froelich to install and use AntConc](https://programminghistorian.org/en/lessons/corpus-analysis-with-antconc), but give it a try on [this corpus of historical documents I have prepared for you](https://craftingdh.netlify.app/data/nls-text-chapbooks.zip) (right-click that link and save-as). This corpus comes from the National Library of Scotland [collection of chapbooks printed in Scotland](https://data.nls.uk/data/digitised-collections/chapbooks-printed-in-scotland/). The data is the OCR'd text from more than 3000 chapbooks, mostly from the 18th and 19th centuries. A chapbook was a cheaply printed booklet, and dealt with popular subjects. Think of them as the checkout aisle magazines of their day.

The data is zipped; unzip it and then you can load it into AntConc. This [file](/data/chapbooks-inventory.csv) contains the metadata for the chapbooks. You could use this to identify the filenames of particular kinds of works you might be interested in, and then copy just those files into a new directory for exploration with AntConc.

To give you an idea of how rich an analysis with AntConc could be, check out [this example concerning 1990s juvenile literature](https://datasittersclub.github.io/site/dsc4/) in ways that would be completely comparable for eg scottish chapbooks database.

Lang, Anouk. "DSC #4: AntConc Saves the Day."" The Data-Sitters Club. April 10, 2020. [https://datasittersclub.github.io/site/dsc4/](https://datasittersclub.github.io/site/dsc4/).

![screenshot of antconc](https://programminghistorian.org/images/corpus-analysis-with-antconc/sorting-shot-1l1r.png)


### Going Further

You can try to perform some of the same kinds of analysis in Python; open the notebook and jump to step 2.1 and follow along for more analysis on materials from the National Library of Scotland.

[Jupyter Notebook by Beatrice Alex](https://htmlpreview.github.io/?https://github.com/bea-alex/DH-MSc-POStagging-lesson/blob/master/POStagging.html).
