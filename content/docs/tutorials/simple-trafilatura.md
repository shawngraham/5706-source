## Trafilatura to scrape data

I found a new tool for scraping materials from the web, called 'trafilatura' - https://trafilatura.readthedocs.io/en/latest/index.html. . Basically, in powershell, terminal, you install it with pip install trafilatura and then you can use it in a variety of ways. Easiest way is at the command line, eg trafilatura -u 'full-url-to-scrape'

But if you run that command, it will print the results to your window. You want them into a file.

trafilatura -u 'full-url-to-scrape' > results.txt

trafilatura -u 'full-url-to-scrape' >> results.txt 

What's the difference here? the > character means write to file - and if you ran the scrape again on a new URL buit kept the > results.txt, it would _overwrite_ your work!

The >> means 'append to file'. So if you changed the url but kept >> results.txt, it would _add_ the results at the end.


So in the screenshot above, I've scraped the search results page from the Canadian Patents 1869-1919 database at LAC (https://www.bac-lac.gc.ca/eng/discover/patents-1869-1919/Pages/list.aspx?PatentTitleEn=cattle&).  See those first numbers after each person's name? Those are unique ids to the various patents and can be plugged into another URL, eg, 3089 is at https://www.bac-lac.gc.ca/eng/discover/patents-1869-1919/Pages/item.aspx?IdNumber=3089& . So, knowing a bit of regular expressions, you could save the results of the scrape to a file, and then put commas around those four digit numbers. Open it in excel, and copy and paste that list of numbers to a new text document, and then use the python script we developed for working with wget to make a list of the full urls with each unique ID, and then get WGET to power through that list, saving any images it finds... ta da!

on the command line, something like this: trafilatura -u "https://www.bac-lac.gc.ca/eng/discover/patents-1869-1919/Pages/list.aspx?PatentTitleEn=cattle&" > results.txt The > character pipes the output of the command into a new file called results.txt. If you wanted to run a different command and append the results to the existing file, you'd use >> instead.

when you open that, in this particular case, there are some existing commas. So we'll delete them, replacing them with nothing...

find: `,`
replace:

then we'll make a regular expression to identify strings of four digits at the end of a line, and put commas around that

thus: ( ) means the pattern inside will be identified as a group
[0-9] means any digit, 0 to 9; the {4} means 4 consecutive of whatever immediately preceeds it
and the $ at the end means anchored to the end of the line.

find: ```([0-9]){4}$)```
replace: `,$1,`

Nothing wrong with using Excel to see how it's going; we've now got those identifiers in their own column, so copy that column into a new text document

And we'll delete the _empty_ lines with another regular expression:

the ^ anchors to the front of the line; the \n means a newline character

find: `^\n`
replace:

and now you have a list of idnetifiers that you can use with the python scripts you learned for wget
