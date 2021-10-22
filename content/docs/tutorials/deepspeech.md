---
title: "Automatic Transcription"
description: "Use a neural network model to transcribe audio recordings automatically"
lead: "It's not perfect, but if you've got a lot of material, it'll get you well on your way."
date: 2020-11-12T15:22:20+01:00
lastmod: 2020-11-12T15:22:20+01:00
draft: false
images: []
menu:
  docs:
    parent: "tutorials"
weight: 783
toc: true
---

## Using Mozilla DeepSpeech to Transcribe Audio

As a historian, it may happen that you have a number of audio files (such as recordings for an oral history project) that you need to transcribe so that you can better search or study the materials.

There is no substitute for listening carefully and transcribing manually (to capture inflections and silences and so on) but there may be times when you do need to give yourself a head start. There are a variety of speech-to-text technologies one might use, but in this walk through, we're going to use a pre-trained neural network model trained on an enormous corpus of transcribed audio. This particular neural network approach handles 'noisy' data [Hannun et al, 2014](https://arxiv.org/abs/1412.5567) and is the basis for [Mozilla's Deep Speech model](https://deepspeech.readthedocs.io/en/r0.9/?badge=latest).

To use it, we'll need a folder of audio files. These get run through the neural network model file, and evaluated against the 'scorer' file, to transform audio signals into English text.

The code that Mozilla provides can be tweaked, optimized, and re-trained for a different alphabet and so on; all of that is beyond the purview of this document.

Here, I'm assuming you have English audio to be transcribed into English text.

## Set up a new 'environment'

I'm assuming you have Anaconda or Minconda on your machine. We want to make a new 'environment' in order to install all the bits and pieces DeepSpeech needs, without interfering with other packages you might have installed.

Open your terminal or anaconda command prompt and create a new environment:

```
conda create --name transcribe python=3.8
```

Accept all the defaults. You're creating a folder on your machine into which everything you'll need is installed. Then, we'll tell your machine to use the python etc in _that_ folder to run the commands you'll give it. When we're done, you'll tell your machine to _stop_ using that folder and to revert back to your default python. Thus:

```
conda activate transcribe
```
when we want to start using DeepSpeech, and

```
conda deactivate transcribe
```

when we're finished. Incidentally, you can get a list of all the _environments_ on your machine with ```conda env list```.

## Install DeepSpeech Code

Mozilla makes a python package for interacting with its models. We can use ```pip3``` to get what we need:

```
pip3 install deepspeech
```

Then, we can get the model file and the scorer with `curl` or `wget`:

```
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/deepspeech-0.9.3-models.pbmm
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/deepspeech-0.9.3-models.scorer
```

or eg `wget https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/deepspeech-0.9.3-models.scorer`

These are very large files, by the way, and depending on your connection, might take a bit of time.

## Prepare your files

Now, if your files are already in `*.wav` format, you're good to go. But if they're not, `ffmpeg` is your friend. Windows users, [follow these steps](https://www.wikihow.com/Install-FFmpeg-on-Windows). Mac users can use Homebrew: `brew install ffmpeg`.

Let's assume you, like me, have a folder of mp4 files. Open a command prompt/terminal prompt in that folder. The following one liner looks for every file in the folder that has the mp4 file extension. It then calls on ffmpeg to transform the mp4 into a wav file, one at a time, and preserves the file name so you know which .wav derives from which .mp4. And then, having done all that, the iteration is closed with the `done`.

```bash
for f in *.mp4;do ffmpeg -i "$f" -vn "${f%mp4}.wav";done
```

Select all the wav files and move them into their own folder. I would suggest having things arranged like this:

```
-deepspeech-work
  |
  |-original-mp4-files
  |-converted-wav-files
  |-deepspeech-0.9.3-models.pbmm
  |-deepspeech-0.9.3-models.scorer
```

**nb** Technically, Deepspeech is expecting a wav file, mono channel, with 16kz sampling. If when you run the commands in the 'Transcribe' sections below and you get some kind of error about your wav file, that might be the issue. You can convert your file appropriately with ffmpeg like this:

`ffmpeg -i file-to-be-fixed.wav -acodec pcm_s161e -ac 1 -ar 16000 fixed-version.wav`

That command tells ffmpeg to take `file-to-be-fixed.wav`, apply some transformations to mix the audio down to a mono channel, and then sample the results at 16 kz and write it to a new file, `fixed-version.wav`.

## Transcribe One File!

First, I'll show you how to use DeepSpeech on _one_ file; you'll do this to get a sense of how it works, and how long things will take.

In what follows, I'm assuming you have your files/folders arranged as in my example above.

Make sure, in your terminal or command prompt, that you are in your `deepspeech-work` folder. At the prompt, we use the `deepspeech` command (that we installed with `pip3` earlier). We tell it which model to use, which scorer to use, and then which audio-file to drop through the whole process:

```python
deepspeech --model deepspeech-0.9.3-models.pbmm --scorer deepspeech-0.9.3-models.scorer --audio converted-wav-files/example1.wav
```

After a few moments, you'll see text being printed into your terminal/command prompt window. Hooray!

## Transcribe Many Files!

Now we want to run the command and have it iterate over every file in the folder. Not only that, we want it to write the text to a file, rather than the terminal/command prompt window. AND we want it to add the result to a text file, and use the audio file's name as a header in the resulting text file. We're going to use a combination of that 'for f in *.mp4' business from before, with the deepspeech command.

Assuming you're in the `deepspeech-work` folder, we do this:


```python
for f in converted-wav-files/*.wav;do deepspeech --model deepspeech-0.9.3-models.pbmm --scorer deepspeech-0.9.3-models.scorer --audio "$f" >> result.txt; echo -e "$f" >> text.txt; done
```
The first part tells your machine which files you want to work on and sets up a loop to go through each file in the converted-wav-files; the second part drops each wav file in turn through the model and the scorer; the >> text.txt _appends_ the output into a result.txt file, and then finally echos (copies) the original source file name into the text file, appending it to the bottom. Then the next file gets transcribed.

The resulting file `result.txt` has your transcriptions for your folder!

## Your Next Step

Perhaps you want to bring all of the transcriptions into R or into Excel. In a text editor, you can use a **regex** find-and-replace the phrase `\nconverted-wav-files/` with say the | character. That is, the machine understands here that when you use `\n` at the start of your search pattern that you mean for it to find `converted-wav-files/` at the start of every 'new line' (for more about 'regex' - regular expressions - see the tutorial on [regex](/docs/tutorials/regex)). Then, you replace that pattern with the pipe character `|`.

eg: you go from this:

```
you messeaged me right yesterday there was a
converted-wav-files/1.wav

that's all folks!
converted-wav-files/2.wav
```
to this:

```
you messaged me right yesterday there was a |1.wav

that's all folks!|2.wav
```
And then you'd save a copy of the file with the .csv file extension.

Then, when you import the file into a different program, you just tell the machine that fields are delimited with the | character.

For instance, if you were then loading the file into R, you might use something like this:

```R
transcriptions <- read.csv("results.csv",sep="|" )
```

Good luck!
