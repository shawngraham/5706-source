---
title: "Simple Photogrammetry"
description: "Building 3d models from photographs."
lead: "Photogrammetry has become much easier in recent years but it is not without its challenges."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 800
toc: true
---

### Introduction

Photogrammetry is the process whereby multiple photographs of an object are stitched together to make a 3d model of the object; the photographs are then draped over the model to make it photorealistic. Because of the physics of photography (focal distances of lenses and so on) a computer can calculate the relative positioning of overlapping points it identifies in multiple photographs, and with a bit of trig it works out the points-in-space. Then it joins these points up by connecting to the nearest neighbouring points, creating a series of triangles or 'mesh'.

A common digital format then for these models is a folder with a .obj file describing the geometry of the object, a .png file with all of the texture information, and a .mtl file that tells the computer how to drape the texture onto the model. Services like [sketchfab.com](https://sketchfab.com) let you upload a zip file of such a folder, and then display or annotate the object. Here's one I did of a gravestone of one of the Moodie family burials:

<div class="sketchfab-embed-wrapper">
    <iframe title="A 3D model" width="640" height="480" src="https://sketchfab.com/models/c287761136a8421ca9856edf8efd595e/embed?autostart=1&amp;ui_controls=1&amp;ui_infos=1&amp;ui_inspector=1&amp;ui_stop=1&amp;ui_watermark=1&amp;ui_watermark_link=1" frameborder="0" allow="autoplay; fullscreen; vr" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
    <p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
        <a href="https://sketchfab.com/3d-models/gravestone2-c287761136a8421ca9856edf8efd595e?utm_medium=embed&utm_source=website&utm_campaign=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Gravestone2</a>
        by <a href="https://sketchfab.com/electricarchaeo?utm_medium=embed&utm_source=website&utm_campaign=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">electricarchaeo</a>
        on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campaign=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
    </p>
</div>

### Getting Started

1. [Read the small section on photogrammetry in ODATE](https://o-date.github.io/draft/book/d-photogrammetry.html)

2. Try making a model of an object in your house; choose something not too shiny, lots of contrast.

If you have an actual digital camera, use that. If you don't, your cell phone camera can work. If you have an iPhone 12 there is an actual app for doing all of this that might obviate all the rest of the steps here. Let me know if this applies to you. Otherwise... you will need to take photos of all sides of the stone/object such that you have sufficient overlap of each image. Around 20 photographs can do it. You might circle the object three times, once at a low level, once at the middle, and once around the top (if feasible).

3. Transfer your photographs to a folder on your computer; if you have a google drive account, you might want to move them there.

4. An actual digital camera embeds metadata about focal length in each image that the photogrammetry process will use. Most cellphone cameras do not. If you are using cellphone images, [please follow these instructions to embed metadata into your images](https://github.com/shawngraham/hist3812w18/wiki/How-do-I-add-metadata-to-my-own-pictures%3F-I-know-I-need-this-to-use-Regard3d-to-make-my-model). This metadata is crucial for the various algorithms to work out how the images relate to one another.

### Making a 3d model

You have two options here.

1. Use Google's own computing resources to stitch a model together for you with a piece of software called 'Meshroom'. To do this, right-click and [open this notebook](https://colab.research.google.com/github/o-date/photogrammetry/blob/master/Meshroom_%2B_GPU_for_Photogrammetry.ipynb) in a new window. You run each cell in that notebook starting at the top - select the cell, then hit run. When it finishes, select the next cell, and hit run. **That notebook has instructions on uploading your images directly, or connecting to your google drive folder**. Read carefully before hitting run! The process might take a bit of time.

2. Download and use Regard3d, an open source collection of algorithms for making 3d models, on your own computer. [Download Regard3](http://regard3d.org/index.php/download) and then follow [its tutorial](http://www.regard3d.org/index.php/documentation/tutorial); you can then re-do its steps on the folder of your own images. Remember: you need to add the metadata to your photos if the camera you used isn't a standard camera.

Then, once you're done:

+ Upload your finished model to [Sketchfab.com](https://sketchfab.com); the free version only allows 1 upload per month. Another option is [https://p3d.in](https://p3d.in); models there can only be max 100 mb in size. There are other options too that you can find with a bit of googling. It might well be that your model is quite wonky - perhaps you didn't have enough photos in the right places. How is the process of taking photographs similar to the kind of close reading you might do in a history class?

+ You can also drag and drop your model files (.obj, .mtl, .png) into a github repo (zipped file is ok too).
