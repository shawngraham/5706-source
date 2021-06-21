---
title: "Markdown"
description: "Futureproofing your writing"
lead: "Separate the <i>content</i> of what you write from the <i>container</i> to enable long term preservation."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 710
toc: true
---

## Introduction

Have you ever fought with Word or another word processor, trying to get things just right? Word processing is a mess. It conflates writing with typesetting and layout. Sometimes, you just want to get the words out. Other times, you want to make your writing as accessible as possible... but your intended recipient can't open your file, because they don't use the same word processor. Or perhaps you wrote up some great notes that you'd love to have in a slideshow; but you can't, because copying and pasting preserves a whole lot of extra gunk that messes up your materials.

The answer is to separate your content from your tool.

This is where the **Markdown syntax shines**. Markdown is a syntax for marking semantic elements within a document explicitly, not in some hidden layer. The idea is to identify units that are meaningful to humans, like titles, sections, subsections, footnotes, and illustrations. At the very least, your files will always remain comprehensible to you, even if the editor you are currently using stops working or "goes out of business."

So: a simple text document using markdown syntax can be read by any device now and into the future. By convention, we change the file extension for any such files to `.md`. A file extension merely signals what kind of program should be used to open the file.

Markdown documents can be dropped through templates of various sources, and turned into Word (for typesetting), pdfs (for sharing), slideshows, html... lots of possibilities. This website, for instance, is built from a series of markdown documents. A commonly used tool for turning markdown text into a variety of file types is [pandoc](https://pandoc.org/).

Markdown can be mixed with code, and used to create documents that have the narrative and the analytical _process_ in a single place. These kinds of documents are the basis for reproducible research workflows. Ben Marwick uses these sorts of documents in his teaching, to encourage students to re-run and re-evaluate the published analyses of archaeologists. But you're historians, right? Why would you want to do this?

Main reason: if you do any kind of digital analysis, no one should believe your results/interpretation if they can't see what you did to the underlying information. Whether the work you do revolves around text analysis (discourses over time over massive corpora!) or social networks (tens of thousands of letters!) or quantitative work (census, historical demographics), markdown plus code repositories (or markdown + code within the document) enables trust. And if people can see how you did your work, they can reproduce the analysis on different bodies of evidence, which means the impact of your work is also increased.

For now, we'll just concentrate on Markdown (but if you want to see how text and code might mix together, a productive example is this [textbook by Melanie Walsh](https://melaniewalsh.github.io/Intro-Cultural-Analytics/welcome.html) and this companion website by [Sharon Leon](http://sharonhoward.org/llb_code/index.html).)

You can find another tutorial on Markdown for historians [here, by Sarah Simpkin](https://programminghistorian.org/en/lessons/getting-started-with-markdown), and a further discussion on 'Sustainable Authorship in Plain Text using Pandoc and Markdown' [here](https://programminghistorian.org/en/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown) by Dennis Tenen and Grant Wythoff.

## Conventions

Here are the main conventions:

**Headers**

`# A Level 1 Heading`

`## A Level 2 Heading`

`### A Level 3 Heading`

**Bullets**

`+ a bullet point`

`1. a numbered bullet point`

**Emphasis**
`_Text_`
	Displays text in italics
`**Text**`
	Displays the text in bold
`**_Text_**`
	Displays the text in bold and italics
`~~Text~~`
  Displays the text with a strikethrough effect

**Links & Images**

`[text link](https://duckduckgo.com)`

`![alt text](https://github.com/n48.png)`

Writing in this way liberates the author from the tool. Markdown can be written in any plain text editor. When you add a `.md` file to Github, Github understands the conventions and turns your plain text into a properly formatted webpage in html. Markdown is currently enjoying a period of growth, not just as as means for writing scholarly papers but as a convention for online editing in general.

> **NB A text editor is different from the default notepad app that comes with Windows or Mac. A text editor shows you exactly what is in a file, including tags, code, and other 'hidden' markup. I suggest you install [Sublime Text](https://sublimetext.com) or [Atom](https://atom.io).**

## Practice

In this exercise, I want you to become familiar with Markdown syntax. (Feel free to check out [Sarah Simpkin's quick primer on Markdown](http://programminghistorian.org/lessons/getting-started-with-markdown)).

_Having already downloaded and installed either Sublime or Atom..._

Have the [Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) open in a new window.

1. Make a new folder on your machine; you'll save your work into that folder. Open your text editor.

2. Using markdown conventions, write a short paragraph on your favourite piece of academic work you've completed so far. Save it in that new folder. The important thing here is to use a variety of markdown conventions so that you get used to the idea.

3. Grab at least two Creative Commons images. The Creative Commons license allows re-use. You can [search for Creative Commons licensed images here](https://search.creativecommons.org/). Download them to your computer, and put them in the folder you are working in. Then use a markdown image link to insert them into your document. **Nb** the images won't appear just yet, so don't worry. An image link for an image in the same folder as the markdown file will look something like this:

`![title of the picture if you know it](image-filename.png)`

4. Add a few hyperlinks to relevant websites.

5. Make sure that when you save your document, you use the `.md` file extension.

You'll finish this exercise by adding your folder to your Github repository. You might need to pause now, and go read the relevant Github materials.

6. Push your folder to Github once you've got your repository set up.

Moving forward, this is how I want you to keep any log files etc that you create in this coruse.
