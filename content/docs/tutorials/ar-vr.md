---
title: "Basic web-based AR/VR "
description: "If you've built a 3d moel, use AR/VR to deliver them"
lead: "Once you've created a 3d model, getting the model into an experience for your public is a bit more difficult."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 805
toc: true
---

### Introduction

I read a lot of science fiction when I was a kid. Augmented and virtual realities were always a part of the scene, in the stuff I read. I've spent a lot of time over the past ten years or so trying to bring those visions to life, given the level of my tech chops and the available technologies I had to play with, with various degrees of success. I shelled out for an Oculus Rift SDK v2, put it on, plumbed it into Minecraft, and promptly had to lie down for three hours because my head went one way and my body went the other.

I get motion sick.

VR just doesn't work for me (maybe with faster frame rates, but who wants to chance it?) But AR - and other kinds of 'mixed' realities - seems to me to hold out much more promise. When I have gone field walking with accomplished landscape archaeologists, they _see_ so much more than I do, because they know how to read the landscape, and their imaginations, training, and knowledge come together to build up a vision of the space that is far more full than what I can see. [Stu Eve](http://www.dead-mens-eyes.org/) wrote his PhD thesis using augmented reality to understand the Bronze Age landscapes of [Bodmin Moor](https://www.barpublishing.com/dead-mens-eyes-embodied-gis-mixed-reality-and-landscape-archaeology.html), and his work is fascinating; well worth checking out. That work used early iPads as a kind of hand-held window into the past. Hand-held AR - well, it doesn't make me motion sick, and if we think of these devices as [opening magic windows](https://emotiveproject.eu/index.php/what-we-do/experiences/) (link is to a mixed reality demo by the Emotive Project at York U in the UK)... I can get behind that.

[A few years ago I wrote](https://electricarchaeology.ca/2015/07/16/the-diary-in-the-attic/)

> The thing about hand-held AR is that you have to account for *why*. Why this device? Why are you looking through it at a page, or a bill board, or a magazine, or what-have-you? It’s not at all natural. The various Cardboard-like viewers out there are a step up, in that they free the hands (and with the see-through camera, feel more Geordi LaForge).

> [...] Without the story, it’s just gee-whiz look at what I can do. It’s somehow not authentic. That’s one of the reasons various museum apps that employ AR tricks haven’t really taken off I think. The corollary of this (and I’m just thinking out loud here) is that AR can’t be divorced from the tools and techniques of game based storytelling (narrative/ludology, whatever).

I can teach you the technical elements of putting together a simple augmented reality web-app. But the storytelling, the framing, the 'why am I doing this with my phone' - that's the harder part. In this exercise then, I want you to reuse the 3d model you built in [week 3](/week/3/photogrammetry) and put it into physical space. We're going to use a tool called [AR.js](https://ar-js-org.github.io/AR.js-Docs/) that delivers AR via html. (Other options are possible - [Unity](https://programminghistorian.org/en/lessons/creating-mobile-augmented-reality-experiences-in-unity) for instance can be used to make both location based and image-based AR).

#### Some terms:

Location based AR: your device reads your position in physical space and overlays 'assets' (3d models, audio, video, text) tied to those spaces

Marker based AR: your device recognizes a marker graphic (like a QR code) and overlays the assets on that marker

Image based AR: your device recognizes distinct images (paintings, photos, logos, etc) and overlays the assets tied to that image ([here's an example from MoMA](https://www.vice.com/en_us/article/8xd3mg/moma-augmented-reality-exhibit-jackson-pollock-were-from-the-internet); here's an example by [public history grad students at Carleton](https://twitter.com/AydaLoewen/status/1239912094746755072)).

### Location Based Ar with a 3d Model

There are many tutorials out there on using AR.js. We're going to do a modified version of these:

[Akash Kuttappa, 2017](https://medium.com/@akashkuttappa/using-3d-models-with-ar-js-and-a-frame-84d462efe498)

[Nicolò Carpignoli, 2019](https://medium.com/chialab-open-source/build-your-location-based-augmented-reality-web-app-c2442e716564).

And we'll need the [quickstart from AR.js](https://ar-js-org.github.io/AR.js/) itself.

We're going to build a website that you load up on your phone, and which will then read your location and put the 3d model you made into that space (see the [photogrammetry exercise](/docs/tutorials/photogrammetry)). What kind of 'story' will you write to make that action 'sensible' or inevitable or entirely reasonable? What story do you tell to make it compelling to do this?

### Setting things up

1. Download your 3d model from Sketchfab in `gltf` format. This will give you a zipped folder; unzip it.

2. Create a new public repository on github for this exercise; initialize it with a readme file. Call the repo `ar-demo`.

3. Drag and drop the **unzipped** folder for your model into the repo. Commit your changes.

4. Create a new file in that repo and call it `index.html`. **nb** This file lives at the same level as your `readme.md` file, _not_ inside your model folder.

### Building your webpage

5. Now, because we're using a web based technology, we have to load the various scripts that we're going to use. We do that inside the `<head>` tag of the index.html webpage you just created. Put the following code into the file like so:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <title>HIST3000 AR demo</title>
    <script src="https://aframe.io/releases/1.0.4/aframe.min.js"></script>
    <script src="https://unpkg.com/aframe-look-at-component@0.8.0/dist/aframe-look-at-component.min.js"></script>
    <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar-nft.js"></script>
  </head>
```

Those three `<script>` tags tell your browser to reach out and grab the javascript packages that will enable the augmented reality. Commit your changes.

6. Find the location you wish to augment in **decimal degrees**. I sometimes use Google Earth to do this. If you go to Google Earth, and search a location, the latitude and longitude will turn up in your URL. For instance, if I wanted to augment the centre of the Quad at Carleton University, I would search for Carleton U in Google Earth, and then zoom in until I had the quad in the centre of the screen (double clicking in the middle to make sure). This URL [https://earth.google.com/web/search/carleton+university/@45.3823833,-75.69885509,72.33333211a,51.2940786d,35y,0h,0t,0r/data=CigiJgokCUUI4Yny6j5AEbHSDo4ACjlAGfM35yrZKEzAIVBSUjKtRVHA](https://earth.google.com/web/search/carleton+university/@45.3823833,-75.69885509,72.33333211a,51.2940786d,35y,0h,0t,0r/data=CigiJgokCUUI4Yny6j5AEbHSDo4ACjlAGfM35yrZKEzAIVBSUjKtRVHA) shows you exactly what I'm looking at. The bit I want is the bit after `carleton+university/@`, or `45.3823833, -75.69885509`. Copy that somewhere safe.

7. Now we're going to build the `<body>`. If you committed your changes back in step 5, you need to hit the 'edit' button. We'll set up a basic opening <body> tag: `<body style="margin: 0; overflow: hidden;">`

8. Now we'll start defining some of the AR.js tags that will deliver us some augmented reality. We open and define an <a-scene> tag:
```html
    <a-scene
      vr-mode-ui="enabled: false"
      embedded arjs='sourceType: webcam; sourceWidth:1280; sourceHeight:960; displayWidth: 1280; displayHeight: 960; debugUIEnabled: false;'
    >
```

9. The next bit tells the camera to be aware of rotation: `<a-camera gps-camera rotation-reader> </a-camera>`

10. And now we tell it the location of our 3d model, and where to pin it to the world:

```html
<a-entity
           gltf-model="gravestone3/scene.gltf"
           rotation="0 180 0"
           scale="0.15 0.15 0.15"
           gps-entity-place="latitude: 45.3823833; longitude: -75.69885509;"
           >
      </a-entity>
```

Where I have `gravestone3/scene.gltf` you'll have the folder name for your model. The rotation and scale elements define how the model will look in the physical space.

11. Now we just close the open tags:

```html
</a-scene>
</body>
</html>
```

...and commit our changes. One last element: we have to tell Github to serve this page up on the web. Go to the cogwheel 'settings' icon and scroll down to `Github Pages`. Under the drop down under 'Source' select 'Master'. Github will build the html and make it available at a location (it'll reload and say 'your page is published at...') which will most likely be `your-username.github.io/ar-demo/` . Grab your smartphone, fire up its browser (Firefox works well) and go to that URL. Give it permission to access your location and backwards facing camera. Carefully scan around you, slowly... your model should appear! (Assuming you're standing more or less at the location whose coordinates you added).

### Conclusion

This is a very basic example of something that could be done. If you explore the tutorial links I shared up above, you should be able to build more complex experiences. You could, for instance, set up _relative_ positioning, so that assets appear in space relative to the user, wherever they may be. You could then code in _all_ of your gravestones, and bring the graveyard to your users. You could set things up so that text or location markers appear. You could set things up so that audio plays, and the voices of the dead whisper to you...

{{< youtube wAdbynt4gyw >}}

(For more about this video, see ['Hearing the Past'](https://www.jstor.org/stable/pdf/j.ctvnjbdr0.15.pdf).)
