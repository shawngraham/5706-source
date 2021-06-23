---
title: "Build an Image Classifier"
description: "Use transfer learning to teach a neural network to recognize objects it hasn't met before."
lead: "Here we retrain the last layer in a neural network to recognize objects of interest that it has not seen before."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 860
toc: true
---

### Introduction

To be honest, I'm having trouble imagining why a historian might want to build an image classifier, but who am I to judge? [Archaeologists are easier to imagine](https://www.eurekalert.org/pub_releases/2021-05/nau-atc051721.php).

A neural network only applies labels at the last layer of its network. We can insert our own labelled image data at that stage, so that we 1) avoid the huge monetary and energy cost of training a new network from scratch 2) reduce the number of examples we have to show the machine before it 'learns' what a particular object is.

Here is [a classifier that I am experimenting with for classifying taphonomic processes on human remains](https://mybinder.org/v2/gh/shawngraham/taph/HEAD?urlpath=apps%2Fclassify.ipynb) (ie, whether they've been burned, suffered water damage, animal damage, etc). It 'works' in the sense that the code executes properly and you get a result - but beware! There are [serious ethical issues at play](https://intarch.ac.uk/journal/issue52/5/toc.html). I wouldn't use this particular classifier to actually make any judgements on the processes visible in the images, because it hasn't been trained on a large volume of images yet, and we haven't measured its accuracy yet.

In this tutorial, you are going to retrain a graph, and then you can point it at images to obtain classifications.

### Retrain a graph

First thing you need are several folders of different kinds of images in the domains you are interested in. Say you're into Ontario's architectural history. You'd make a series of folders for different kinds of architectural styles - Gothic, Queen-Ann, Italianate, Arts-and-Crafts.

Into each of those folders, you would place several examples of each style (as many as you've got, really, but for the purposes of this exercise, aim for at least twenty each), in jpg format.

Then, download a copy of my code repo at [https://github.com/o-date/image-classifier](https://github.com/o-date/image-classifier).

Unzip, open the repo, and delete the subfolders in `image-classifier/tf_files/gallery/`

Drag-and-drop your folders into `image-classifier/tf_files/gallery/` ; these are the subfolders you collected that show examples for the different kinds of things we want to classify. The names of the subfolders are the labels that will be applied.

I'm assuming that you have Jupyter notebooks installed. Open a command prompt / terminal in `image-classifier` and start jupyter notebooks: `$ jupyter notebooks`.

On the jupyter page, start the 'Building an archaeological image classifier with tensorflow.ipynb' notebook.

There are only two code blocks (there's a lot of ancillary information in the notebook for your information). The first one invokes the python script that retrains a neural network on the subfolders of materials you put in the gallery folder. Run this block.

### Testing

When it finishes, find _another_ image of Ontario architecture; you're going to test your newly-trained classifier. Put this image in the `image-classifier/tf_files/testing/` folder. Let's say it was called 'ontario-house.jpg'. You would modify the _second_ code block by changing out the filename 'B4-1-f.jpg' for 'ontario-house.jpg', eg:

```
!python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/testing/ontario-house.jpg
```

When you run this second block, a lot of information will print out - warning messages, mostly- and then you'd get your result; something like,

```
2021-06-23 18:33:36.114158: I tensorflow/core/platform/cpu_feature_guard.cc:140] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA

Evaluation time (1-image): 0.194s

Italianate (score=0.99973)
Queen-Ann (score=0.00027)
```
