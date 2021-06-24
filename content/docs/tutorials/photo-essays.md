---
title: "Photo Essays"
description: "Static photo-essay website"
lead: "This is a variant of a static website."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 795
toc: true
---

## Introduction

Sometimes, what you want is a static website that is built around photography or images. Here, we're going to use a _bash script_ to build such a website, drawing on a folder of images on your machine. The result will look <a href="http://jack.ventures/" target="_blank">this</a>. We're going to use the [Expose](https://github.com/Jack000/Expose) site builder by Jack Qiao.

## But first, some dependencies

Imagemagick is a suite of tools for working with images, transforming them, cropping them, and so on _from the command line_. This means that you can set up batch processes, sequences of commands, to work on every file in a folder.

### Mac
To get Imagemagick for the Mac, I am assuming that you have [Homebrew](https://brew.sh/) installed. If not, open up the terminal and paste this command there, and run it:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once that finishes, you can get imagemagick with:

```
brew install imagemagick
```

If you want to have videos in your eventual website, you'll also need FFmpeg:

```
brew install ffmpeg
```

### PC

You can get Imagemagick by right-clicking and 'save-as' this link: [https://download.imagemagick.org/ImageMagick/download/binaries/ImageMagick-7.1.0-1-Q16-HDRI-x64-dll.exe](https://download.imagemagick.org/ImageMagick/download/binaries/ImageMagick-7.1.0-1-Q16-HDRI-x64-dll.exe)

If you want videos on your eventual site, you'll need FFmpeg, which you can get from [here](https://www.ffmpeg.org/download.html#build-windows), but you might want to read through [this guide first](https://www.wikihow.com/Install-FFmpeg-on-Windows) since you'll need to tell your machine where FFmpeg is by adding its location to an environment variable. For the purposes of this tutorial, you might just want to skip working with any videos.

Because Expose is a 'bash' script, windows users will also need a 'bash shell' to run this script. If you have Git install on your windows machine, you're in luck, because a program called 'Git Bash' will have been installed (otherwise [click on this link to download and install git](https://git-scm.com/download/win). **Just use all of the suggested default settings when you run the installer**.)

Once that's finished installing, you can check to see if it's installed by right-clicking on a folder in the file-explorer; one of the options should be 'Git Bash Here'

## Getting Expose

Download the Expose repository at [this link: https://github.com/Jack000/Expose/archive/refs/heads/master.zip](https://github.com/Jack000/Expose/archive/refs/heads/master.zip).

Unzip it somewhere sensible on your machine _and remember the path - location - where it is at_.

### Alias on Mac

Now, if we wanted to turn the `expose.sh` script into a command that your machine can find everywhere (in whatever folder you were working), we have to tell it where to find it.

_Mine_ is in my Documents folder. So, **on a mac**, I type the following in at the terminal:

```
alias expose=~/Documents/expose-master/expose.sh
```

Then, when I invoke `expose` moving forward, the computer will know to look in the expose-master folder in my Documents folder for the `expose.sh` script.

### Alias on PC?

This is possible, but it's too convoluted for our present purposes.

**Windows users** you'll use the bash shell and directly invoke the script by giving the full path every time you want to use it, see below.


## Build the site

Now, at the terminal in your folder of images, run the bash script:

**On a Mac:**

```
./expose.sh
```

**On a PC:**

Find the folder of images you want to turn into a site, in your file explorer. Right-click, and select 'Git Bash Here'.

In the window that opens - which will look very similar to the command prompt window - you will be telling the machine to run the expose.sh script with the `sh` command, so you need to know the location where you put that folder. On my machine, the complete command looks like this:

```
sh C:/Windows/System32/Expose-master/expose.sh
```
I moved the `Expose-master` to the folder `C:\Windows\System32`. I did this, because when I first set up my windows machine, I put a space in the user name. This was a mistake. This means that in many file paths on my machine, eg to folders on my desktop or in my documents folder, there is a space! Spaces in filepaths cause trouble. Always try to avoid them. So I moved the folder to a location where I know there will be no spaces.

Another couple of things to notice there. _Normally_, windows uses `\` in file paths. Bash understands those differently, so use forward slashes `/` in the path. Second thing: we're using the `sh` command to tell windows that this is a SHell script you're running.

### As it builds...

You might get some error messages about image properties; don't worry about that. Just let the script do its work. Eventually it will say `Building HTML`.

When it finishes, there will be a new folder called `_site`. You can view the results of your work by changing directory into there and starting a webserver (Windows users, you should open a anaconda powershell in the _site folder and THEN run the python command).

```
cd _site
python -m http.server 5000
```

If you like what you see, hit ctrl+c in your terminal, and then upload all of the contents of the `_site` folder to a github repo; turn on github pages from the repo settings, make sure that it is building your site from the `main` branch, and ta-da, a photo-essay, online, at your-username.github.io/your-repo .

### Modifying your site

Expose sorts images in alphabetical order by file name. To organize your site then you can either rename the images with a numerical prefix (01-image-this.png, 02-image-that.png ... 12-another-image.png and so on) OR create subfolders, again with numerical prefixes. Any file or folder name leading with an underscore are ignore.

For adding **text** to the images, you create a text file that has a _metadata_ block at the top that gives the coordinates for where you want the text to appear in percentages measured in from the relevant edge.

**The text file must have the same name as the image**, eg, "03-at-the-river.png" and "03-at-the-river.txt". By metadata block, I mean something that starts with a line with three dashes, and finishes with a line with three dashes:

```
---
top: 30
left: 5
width: 30
height: 20
textcolor: #ffffff
---

At the river, we encountered a strange old man who held a fishing rod made from pvc pipes.

```

For more on the various options and theming, see the [repo](https://github.com/Jack000/Expose).

When you make these kinds of changes, you'll need to re-run the `expose.sh` command to rebuild the site. _Don't_ run expose.sh when you're _inside_ the _site folder! Use `cd ..` to get back out of that folder.
