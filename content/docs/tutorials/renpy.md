---
title: "Visual Novels with Ren'Py"
description: "Another game engine"
lead: "Ren'Py is a python based game engine for making Visual Novels; for when the experience you want to craft is more literary, perhaps. Also, an excellent platform for integrating imagery and art with your storytelling."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 790
toc: true
---

## Introduction

[Ren'Py](https://www.renpy.org/) is a 'visual novel engine'. You may have encountered games created with Ren'Py; often these are heavily influenced by Japanese '[dating sims](https://en.wikipedia.org/wiki/Dating_sim)' and often feature anime or anime-inspired artwork. But 'visual novels' are more of a subset of adventure games. In any event, engine does not dictate genre. The Ren'Py engine enables you to combine art, sound, story, and meaningful choices (and all of the variability that that entails) into a package that can be played on Mac, PC, Linux, iOS, Android, and the web, as a standalone game (which has interesting implications for public digital history and accessibility).

[Itch.io](https://itch.io/games/made-with-renpy), a site where all sorts of independently crafted games and immersive experiences may be found, describes Ren'Py like this:

> Ren'Py is a visual novel engine – used by thousands of creators from around the world – that helps you use words, images, and sounds to tell interactive stories that run on computers and mobile devices. These can be both visual novels and life simulation games. The easy to learn script language allows anyone to efficiently write large visual novels, while its Python scripting is enough for complex simulation games.

### Getting Started

Because things can get complicated quite quickly, you might want to sketch out on paper (or even use [twine!](https://twinery.org)) the structure of your story. What do you hope to achieve? Are you trying to invoke a kind of emotional response? Do you want to explore ideas around [inevitability and memory](https://epoiesen.library.carleton.ca/2017/09/01/destory-history/)? What kind of simulation are you creating? If there are puzzles or challenges, what _historiographic_ point do they serve?  

At the link, you can find a demo game that I created called the <a href="/data/Nile_Diary-1.0-web/index.html" target="_blank"> Nile Diary</a>. (I'm not sure where the 'loading' screen in the web distribution comes from, I'd like to change it. Anyway.) The idea of the visual novel was to explore the story of a 19th century socialite's trip to Europe from New York. I had spent quite some time transcribing the diary, and I imagined the visual novel of that trip would be like stepping into the diary, but with interruptions from an unreliable narrator who represented the historian, and so the story becomes not just about a trip to Europe, but also, about how we know things historically. I sketched out the scenes on paper, and the discursive 4th-wall breaks, and some narrative branches where it wasn't clear in the diary what happened in what order. (What I ended up building is only a few scenes long, but it is enough to understand how Ren'Py works.)

Once you have a sense of _how_ you want your story to go, and the main idea you're exploring (and how the rules that you are building - the choices and so on - intersect with your historical consciousness or historiographical approach), then you're ready to build.

Collect the artwork you think you'll need, collect the audio. Make sure it is creative commons licensed, public domain, or your own creations.

### Ren'Py Interface

You can get the development environment [here](https://www.renpy.org/latest.html). Download, install, then open. You'll be presented with the Ren'Py Launcher:

![](/images/renpy/renpy-launcher.png)

Under the 'projects' heading are two novels ready for you to explore - the Tutorial, and The Question. Select the project, and then 'Launch Project' to play them.

The source for these games is inside the renpy folder on your machine, but you can also go there directly by hitting the folders under the 'Open Directory' header, or the relevant script files themselves. `script.rpy` holds the actual story, while the other `rpy` files control various behaviours for the game. The first time you click on any of these, RenPy will ask you to associate a text editor with them. I have Atom installed on my Mac, so I selected that from the options. This also prompts Ren'Py to search for any updates and download them.

Once you've done all that, you can explore the files that make up a game. Select the Tutorial game, and then hit 'Launch Project'. I'd turn my audio down too, if I were you. The first scene loads up with some pretty fun music... (you can mute the audio under the 'preferences' button while the tutorial is running)

The tutorial is quite well done in that it is created in Ren'Py and it demonstrates not just how to interact with a game, but also how to start a new project and then how to write the scripts and so on. I would suggest working through the entire 'Quickstart' section of the tutorial, and then try to make a short story of your own.

The [Ren'Py Documentation](https://www.renpy.org/doc/html/) is extensive and covers pretty much anything you'd like to do.


### Source of the Nile... Game.

The script file for my 'nile' game looks like this (I just used the script in the 'Question' game as my model):

```
# Declare images below this line, using the image statement.
init:
    image bg steamer = "bg_steamer.jpg"
    image bg whale ="bg_whale.jpg"
    image bg sinking ="bg_sinking.jpg"

    image shawn full ="shawn.png"
    image shawn eyesright = "shawn_eyes_right.png"

# Declare characters used by this game.
define tl = Character('The Lady', color="#c8ffc8")
define sg = Character('Shawn', color="#c8c8ff")
```

And then I made the splash screen, the screen that shows up when you first start the game but before the menu:

```
#splash
image splash = "Nile Temple.jpg"

label splashscreen:
    scene black
    with Pause(1)

    play sound "331375__xanco123__mysterious-event-music-01.ogg"

    show splash with dissolve
    with Pause(5)

    scene black with dissolve
    with Pause(2)

    show text "Shawn Graham @electricarchaeo"
    with Pause (2)

    return
```

And then the 'game', such as it is:

```
The game starts here.
label start:

   play music "23722__milo__ship2-bergen.ogg"

   scene bg steamer at Pan((100, 100), (1000, 1000), 20.0)
   with fade

   tl " Left New York in Cunard steamer Algeria."

   stop music

   scene bg whale with fade
   tl "Capt. read serviceon Sunday morning - in afternoon dead body of whale, white and shiny quite near us upon the water and hundreds of little birds upon it"

   scene bg sinking with fade
   tl "The second sunday morning suddenly a great wave rose ten feet above the deck "    
   tl "and came down upon it knocking down every one before it"
   tl  "and came down the gangway."

   show shawn full at left with dissolve

   sg "Wait. Wait."
   sg "You need to know what you're reading here."

   show shawn eyesright at left with dissolve

   sg "And what this is all about."

   menu:

       "Is it a game?":

           jump game

       "Are you telling a story?":

           jump story

label game:
    sg "yep"

    menu:

       "Not much of a game, is it.":

           jump notmuchgame

label story:
    show shawn full at center with dissolve
    sg "more or less"

label notmuchgame:
    scene white
    with dissolve

    sg "well, hang on, ok?"
    sg "this is just me still working through how this platform works."
    show shawn full at center with dissolve
    sg "the idea is that you'll get the story of the Nile Diary"
    sg "but also get 4th-wall breaks that explain what I'm trying to achieve"
    sg "in my research on the diary,"
    sg "the choices I made, the tech I've used, pointers to further info, etc"

    show splash
    sg "stay tuned..."

    return
```

The audio files, the images, the graphics, are all from creative commons or public domain sources. They're kept in the relevant folders. As I make changes to the script, I save the script file and then hit the **Launch Project** button to play through. When I'm ready, I can hit the 'Build' option from the Ren'Py launcher, and create Mac and PC versions and so on for distribution. RenPy also has a beta feature (meaning there might still be bugs) for exporting to the web. I used that feature to build the version I linked to above, and then uploaded the web version to the github repo which powers this site. In your case, you could create a new github repo, enable github pages from the `main` branch of the repo, and then drop the entire contents of the web distribution into that repo.

Have fun!
