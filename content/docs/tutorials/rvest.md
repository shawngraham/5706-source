---
title: "Webscrape with R"
description: "A section from The Macroscope, 2nd edition, on scraping data with R"
lead: "R is a versatile programming language; here we use it to scrape data from the web."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 820
toc: true
---

In the second edition of _Exploring Big Historical Data: The Historian's Macroscope_ we spend some time showing the reader how to scrape historical information from a website using R. This tutorial is derived from that portion of our text. The book should be out in the world sometime in 2022 I expect.

### Introduction

The R programming language is very versatile, and very powerful. Here, we are going to scrape the court records of the Salem Witch Trials, which are online at [http://salem.lib.virginia.edu/category/swp.html](http://salem.lib.virginia.edu/category/swp.html). Go take a look at that site; find a trial docket that interests you. Here, we are going to have to delve into some of the underlying html.

HTML - hypertext markup language - uses a variety of conventions to indicate how the browser should interpret the text in the file. Things like `<a>` indicate hyperlinks, `<b>` indicates bold text, and so on. Any one of these 'tags' can have modifers attached to them that the browser will modify according to elements in the 'css' file (the 'cascading style sheet', where 'cascading' refers to the order in which elements should be modified). All that to say - look at interesting text on the webpage; if you right-click on an interesting element, you can select 'inspect' from the context menu to view the underlying code.

You'll see that all of the links to the actual papers all have roughly the same URL pattern. So our goal is going to be to get the machine to identify and then iterate through that list, saving the text of all those papers _without_ the surrounding html, and saving them as text files on our own machine for further analysis.

So let's get scraping.

### Get R Studio running and make a new 'R script' file

1. From Anaconda Navigator, you can select 'launch R Studio' (hit the 'install' button for R Studio if you haven't all ready). RStudio is a 'development environment' for working with the R language. It will let you write and edit code, run the code, see the current state of any variables you make, display plots or graphs you make, and much more. People often create 'packages' of code for doing particular tasks, and then make them available for other users. We're going to be grabbing some packages for working with websites in a moment.
2. When R Studio starts, select `file > new file > r script` (or, click on the green plus sign beside the R icon). The panel that opens is where we’re going to write our code. Code that you write in this panel does not run until you tell RStudio to run it. You do that by putting your cursor on the line you want to run, then clicking on (or using the key-board shortcut) the ‘run’ button. The code will get passed to the ‘console’ window, and R will run it. When things go wrong, the console is where you’ll see the error messages. Data that gets imported, or variables that get created, will be displayed in the environment window. A file explorer is in the final window.
3. In the **console** window, type `getwd()`. This command - get working directory - tells you which directory on your machine you are working in. You can change this by using the file explorer in the bottom right hand panel of the interface, and then, under the cogwheel more dropdown, selecting 'Set As Working Directory'.
4. In your new script window (where you can edit your script), we're going to write a few lines of code. The first three will install some packages for us; the next three will tell R to _use_ those packages:

```
install.packages("rvest")
install.packages("dplyr")
install.packages("magrittr")
install.packages("stringr")

library(rvest)
library(dplyr)
library(magrittr)
```

To _run_ this code, place your cursor at the start of the first line, and hit the 'run' button at the top of the pane. Alternatively, there are shortcut keys like ctrl+enter or cmd+enter that will run the line, passing the line to the console below, executing it, and then moving the cursor to the next line. As you do this for the `install.packages` command, the console will fill up with information as R Studio reaches out, downloads, and installs the different bits and pieces. Be patient and wait for each line to run before running the next one. When R is doing something, **a little stop sign icon** will appear on the console window. You'll know it's finished when that disappears and the `>` prompt re-appears in the console.

When you run the `library` commands, it might not appear like anything has occurred - the `>` reappears instantaneously. Generally, no news is good news. Once you've run these commands, go back into the script window and put a `#` in front of each `install.packages`. R understands the `#` sign as a line to ignore; we can use the `#` to write comments to ourselves in our code. Since you only need to install these packages once, you can comment them out like this so that when you re-use or modify this script, you don't start installing things all over again.

These four `library` commands tell R that we want to use the `rvest` (say it out loud) and `dplyr` packages to handle scraping data and rearranging data; the `magrittr` packages makes it easier to pass the results of our manipulations from one function to the next (using the ‘pipe’ function, which looks like this: `%>%`).

### Set up some variables

Next thing we'll do is set up some variables. In R, we give the name of the variable, and then use the `<-` to tell R what goes into it. We're going to tell R the URL of the page where we want to grab data, and we're going to also have to tell is what the 'base URL' for the entire site is, so that we can build up our list of pages to scrape properly. Add these two lines to the script, and then run them:

```
base_url <- "http://salem.lib.virginia.edu/"
main_page <- read_html(x = "http://salem.lib.virginia.edu/category/swp.html")
```

### Identify where to find the interesting data in the html

The `rvest` package has some useful functions in it. These commands do things like identify hyperlinks (the [`a` tag](https://www.w3schools.com/tags/tag_a.asp)), the attributes of tags (like `href`, for outgoing links), and the labels for those tags. It will look like this:

```
urls <- main_page %>% 	 	# feed `main_page` to the next step
  html_nodes("a") %>% 	  # get the CSS nodes for a link
  html_attr("href") 	    # extract the URLs from the link

links <- main_page %>% 	  # feed `main_page` to the next step
  html_nodes("a") %>%     # get the CSS nodes
  html_text() 		        # extract the text
```

See what we did there? We are using `#` at the end of each line of code to explain what the line is doing. We are also using the `%>` from the `magrittr` package to feed the results of each line to the next line.

So... that code creates a variable called `urls`. Into `urls` we dump the `main_page` html (R goes out and grabs it all!) and then we use the `html_nodes` command to go through that webpage for all the hyper links, and then look up the 'attribute' for each hyperlink: the actual URL to the resource we want. It does it again for `links` so that we end up with the _link text_ for each. Put your cursor at `urls` and run; it passes the complete 3 lines of code to the console and executes. Do the same again for `links`.

### Create a dataframe with that data

The next step is to take those two variables, and put 'em together to make a table with two columns _also_ called 'links' and 'urls'. Let's call this dataframe, this table, 'reports':

```
reports <- data_frame(links = links, urls = paste(base_url,urls, sep=""), stringsAsFactors = FALSE)
```

Run that line. (The bit with 'stringsAsFactors' is to stop R from thinking that this data is something called a 'factor'. You don't have to worry about this now.)

Now you can see your table by running `View (reports)` in the console (the capital V in `View` is necessary).

See how there is some extra stuff at the top and the bottom of that table? We grabbed a few hyperlinks that we don't want. So we're going to get rid of 'em by counting backwards from the `tail`. So - there are 150 lines of data, but we don't want the first 10, so 150-10 = 140. In your script:

```
reports <- reports %>% tail(140)
```

And run that.

### Loop over all the reports and extract the text to a new directory

To keep things nice and tidy, we're going to create a new subdirectory in the folder you are working in (remember, `getwd()` will tell you what folder you're in if you forget). We do this like so (add to your script):

```
dir.create("reports")
```

Run that.

We're going to build our loop now by create a variable into which we will store everything as R works its way down that list we just created; when it's finished, we'll write all of that information.

```

# Loop over each row in `reports`
for(i in seq(nrow(reports))) {

  text <- read_html(reports$urls[i]) %>% # load the page
    html_nodes(".doc") %>% 			         # isolate the text
    html_text() 					               # get the text

    # Create the file name
    filename <- paste0("reports/", reports$links[i], ".txt")

    #this uses the relevant link text as the file name

    sink(file = filename)     # open file to write
    cat(text)                 # write the data
    sink()                    # close the file

} #end the loop
```

Before you run that, notice that the loop is everything between the `{``}` characters. So the line `for(i in seq(nrow(reports)))` means, for each 'i'tem in 'seq'uence(moving down the rows(in the reports table)).  Then, since I've already inspected the html for one of the reports and know that the full text of every one of the reports is identified with "class=doc" in the html, we use them_nodes to find the text, and then html_text to grab the text. Then we create a filename for each row, using the link text; we open that file, use the `cat` (concatenate) command to write the text to file, and then close it. That takes us to the end of the loop and we do it all again!

Check the 'reports' folder when it's finished (it might seem as if everything has locked up, but just wait. Should run completely within about 2 minutes).

### Now what?

Well, now you could use these files to make a topic model, or maybe some Voyant, or AntConc...

And it might be useful to have all of that data as a single dataframe, depending on what you want to do. Easy:

```
full_reports <- as.data.frame(text)

### and if you want to have it all as a csv file:
write.csv(full_reports, "full-reports.csv")
```
