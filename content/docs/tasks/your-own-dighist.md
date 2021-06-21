---
title: "6. Your Own Digital History"
description: "Instructions concerning a small digital history project you will build."
lead: "In weeks 7 - 11 you will embark on your own digital history 'thing'. Guidelines are on the website. As part of this, you will write three 'devlogs' or updates on the work, the problems you're facing (or have overcome). These help to frame the 'paradata' of your work."
date: 2020-11-12T13:26:54+01:00
lastmod: 2020-11-12T13:26:54+01:00
draft: false
images: []
menu:
  docs:
    parent: "tasks"
weight: 670
toc: true
---

```txt
To be completed within weeks 7 - 11, Nov 1 - Dec 5.
Note the subtasks due within Weeks 7, 9, and 10.
The paradata are due at the end of Week 11.
```

## The Task

Knowing what you now know about some digital methods as well as some of the broader historiographical issues of doing digital history, this next section of the course is your opportunity to push yourself to _build_ a work of exploratory digital history.

To be clear: this means _not_ that you are creating _the_ definitive work of digital history on your particular area, but rather, that you are building something that enables you to explore historical materials digitally sufficiently that you can identify where the big ticket issues or questions might be. DH is a team sport; a work like this would be the kind of thing that enables you to formulate a bigger research project, describe the necessary work to potential collaborators, enable you to figure out budgets, and so on. Conceptually, what I'm asking you to do can be thought of as being a bit like [an artist's cartoon](https://en.wikipedia.org/wiki/Cartoon#Fine_art):

> _A cartoon (from Italian: cartone and Dutch: karton—words describing strong, heavy paper or pasteboard) is a full-size drawing made on sturdy paper as a design or_ modello _for a painting, stained glass, or tapestry. Cartoons were typically used in the production of frescoes, to accurately link the component parts of the composition when painted on damp plaster over a series of days (giornate). In media such as stained tapestry or stained glass, the cartoon was handed over by the artist to the skilled craftsmen who produced the final work._

_Capisce?_

### Subtasks

You will need to

- identify a source of data of interest, and why
- clean / wrangle it sufficiently to work with it, documenting the choices you make along the way, reflecting on how that is affecting what you might eventually find/do
- do some exploratory analysis or visualization of the material, contextualizing for us what this might mean.

- you will create a private or public Github repository for this work. All materials that you create should be deposited. I recommend you keep daily notes or a log of what you are doing and why, including errors and so on - not for me to grade, but for me (or your peers) to help you troubleshoot.

### Outputs

- 3 devlogs, at the end of **Week 7**, **Week 9**, and **Week 10**. A devlog, for our purposes, will be a post in the relevant discord channel that sums up your progress to that point (use bold text in your post eg: **Shawn's Devlog 2, Nov 17**). These do not need to be overly long. A couple of paragraphs is fine.

### Completion Date

- Share, and make public your _paradata_ (ie, the narrative explaining what you've done, the decisions you've made, the work you've done/learned how to do, why it might matter historically) using Github Pages **by the end of Week 11.**

- Post the link to the relevant Discord channel

## Potential Data Sources

_A non-exhaustive list_

### Ottawa Datasets

#### Galleries
- National scale
  - [Inuit Artists' Print Database](https://www.gallery.ca/inuit_artists/home.jsp?Lang=EN)
  - [Art in Canada to 1930](https://www.gallery.ca/indexartcanada/home.jsp?Lang=EN)
  - [Canadian Souvenir View Albums](https://www.gallery.ca/sva/intro_e.htm)
  - [NGC Database](http://archives.gallery.ca/?lang=en)
  - [Artists in Canada](https://app.pch.gc.ca/application/aac-aic/?lang=en)


#### Libraries & Archives
- LAC
  - [Notebook](https://nbviewer.jupyter.org/github/GLAM-Workbench/library-archives-canada/blob/master/lac-naturalisation-1915-1945-harvest-by-country.ipynb) that creates datasets from [LAC Naturalization Records, 1915-1946](https://www.bac-lac.gc.ca/eng/discover/immigration/citizenship-naturalization-records/naturalized-records-1915-1951/Pages/introduction.aspx) --> could likely be repurposed to extract later records as well
  - [Black Loyalist Refugees, 1782-1807- Port Roseway Associates](https://www.bac-lac.gc.ca/eng/discover/military-heritage/loyalists/loyalist-port-roseway/Pages/port-roseway-associates-loyalists.aspx)
  - [Canadian Illustrated News, 1869-1883](https://www.bac-lac.gc.ca/eng/discover/canadian-illustrated-news-1869-1883/Pages/canadian-illustrated-news.aspx)
  - [Canadian Patents, 1869-1919](https://www.bac-lac.gc.ca/eng/discover/patents-1869-1919/Pages/canadian-patents-1869-1919.aspx)
  - [Carleton Papers – Book of Negroes, 1783](https://www.bac-lac.gc.ca/eng/discover/military-heritage/loyalists/book-of-negroes/Pages/introduction.aspx)
  - [Carleton Papers – Loyalists and British Soldiers, 1772-1784](https://www.bac-lac.gc.ca/eng/discover/military-heritage/loyalists/loyalists-british-soldiers-1722-1784/Pages/introduction.aspx)
  - [Immigrants Before 1865](https://www.bac-lac.gc.ca/eng/discover/immigration/immigration-records/immigrants-before-1865/Pages/introduction.aspx)
  - [Immigrants from the Russian Empire, 1898-1922](https://www.bac-lac.gc.ca/eng/discover/immigration/immigration-records/immigrants-russian-empire/Pages/introduction.aspx)
  - [Ukrainian Immigrants, 1891-1930](https://www.bac-lac.gc.ca/eng/discover/immigration/immigration-records/immigrants-ukraine-1891-1930/Pages/introduction.aspx)
  - [Marriage Bonds, 1779-1858 - Upper & Lower Canada](https://www.bac-lac.gc.ca/eng/discover/vital-statistics-births-marriages-deaths/marriage-bonds/Pages/marriage-bonds-upper-lower.aspx)
  - [Open Data](https://search.open.canada.ca/en/od/?sort=score%20desc&page=1&search_text=&od-search-subjects=History%20and%20Archaeology&od-search-format=CSV)

- [City of Ottawa Archives](http://ottawa.minisisinc.com/ottawa/scripts/mwimain.dll?logon&application=UNION_SEARCH&language=144&file=[ottawa_web]NewOPAC\index.html)
  - Offers collections of artworks and items from Ottawa historical museums --> cannot find exportable data, would have to be scraped

- [Canadiana.ca](https://www.canadiana.ca/)

#### Museums

- [Canadian Museum of History](https://www.historymuseum.ca/collections/)

- Ingenium Museum Network
  - [Open data](https://ingeniumcanada.org/collection-research/artifact-open-data-set-mash-up)
    - All artifacts in the collection of the Canada Agriculture and Food Museum, Canada Aviation and Space Museum and the Canada Science and Technology Museum
    - Available in XML or CSV
