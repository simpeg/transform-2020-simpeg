**[summary](#summary) | [prerequisites](#prerequisites) | [setup](#setup) | [resources](#resources) | [license](#license)**

# Transform 2020: Geophysical inversions with SimPEG

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/simpeg/transform-2020-simpeg/main)
[![License](https://img.shields.io/github/license/simpeg/transform-2020-simpeg.svg)](https://github.com/simpeg/transform-2020-simpeg/blob/main/LICENSE)

|         | Info |
|--------:|:-----|
| When    | Tuesday, June 9 • 12:00 - 15:00 UTC |
| Slack   | [Software Underground](https://softwareunderground.org/) channel `t20-tue-simpeg` |
| YouTube | https://youtu.be/jZ7Sj9cnnso |
| conda environment  | `t20-tue-simpeg` |
| Intro Slides  | [SimPEG Transform presentation](https://docs.google.com/presentation/d/1Iw0chJUvjaiuGpQIqiYal719pcvWD2xs2z2aXkpQThQ/edit?usp=sharing) |

**Team**
- [Lindsey Heagy](http://github.com/lheagy) (Instructor)
- [Seogi Kang](https://github.com/sgkang)
- [Joe Capriotti](https://github.com/jcapriot)
- [Dom Fournier](https://github.com/fourndo)
- [John Kuttai](https://github.com/JKutt)
- [Dieter Werthmüller](http://github.com/prisae)
- [Doug Oldenburg](http://github.com/dougoldenburg)
- and the [SimPEG contributors](https://github.com/simpeg/simpeg/graphs/contributors)

## Before the tutorial

Make sure you've done these things before the tutorial on Tuesday:

1. Sign-up for the [Software Underground Slack](https://softwareunderground.org/slack)
1. Join the channel `t20-tue-simpeg`. This is where **all communication will happen**.
1. Set up your computer ([instructions below](#usage)). We will not have time to
   solve many computer issues during the tutorial so make sure you do this
   ahead of time. If you need any help, ask at the `t20-tue-simpeg` channel on
   Slack.
1. If you have some data you'd like to process, please have it ready and make
   sure you can load it with pandas or numpy. You'll have some time at the end
   of the tutorial to work on your own data.

## Summary

This repo contains the notebooks and tutorial resources for the Transform 2020 tutorial on Simulations and inversions with SimPEG.

- [Session Description](https://transform2020.sched.com/event/cD5V/tutorial-geophysical-inversion-in-simpeg)
- [Intro Slides](https://docs.google.com/presentation/d/1Iw0chJUvjaiuGpQIqiYal719pcvWD2xs2z2aXkpQThQ/edit?usp=sharing)

In this tutorial, we will provide a hand-on overview of using SimPEG to simulate and invert geophysical data. The examples we plan to work through use Direct Current (DC) Resistivity and Induced Polarization (IP) data from the Century Zinc Deposit in Australia.

Starting from field data in a text file we will learn how to
- load those data into SimPEG
- construct a survey object that contains the geometry of the sources and receivers
- set up and run a forward simulation
- define the inverse problem consisting of a data misfit and regularization
- run an inversion and discuss inversion strategies

Then, we will work with a synthetic example to
- demonstrate how to explore aspects of the physics with SimPEG
- explore the role and influence of parameters used in an inversion

## Prerequisites

**Software**

* Some knowledge of Python is assumed (for example, you might want to attend the
  [getting started with python](https://transform2020.sched.com/event/c7Jm/getting-started-with-python) or
  [more python for subsurface](https://transform2020.sched.com/event/c7Jn/more-python-for-subsurface) tutorials).
* All coding will be done in Jupyter notebooks. I'll explain how they work
  briefly but it will help if you've used them before.
* We'll use [numpy](https://numpy.org/), [matplotlib](https://matplotlib.org/), and
  [ipywidgets](https://ipywidgets.readthedocs.io/)
  You don't need to be an expert in these tools but some familiarity will help.

**Geophysical Inversions**

* This tutorial will focus on Direct Current (DC) Resistivity and Induced Polarization (IP).
  I'll explain the basic principles, but if these are new to you, then I would recommend
  taking a read through the [DC Resistivity](https://gpg.geosci.xyz/content/DC_resistivity/index.html)
  and [Induced Polarization](https://gpg.geosci.xyz/content/induced_polarization/index.html) sections
  of the [Geophysics for Practicing Geoscientists resource](https://gpg.geosci.xyz/index.html)
* Similarly, I do not assume an extensive background in inversions, but it will help if you have been
  introduced to some concepts. The [GIFTools Cookbook](https://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/index.html)
  provides a nice overview.

## Usage

There are a few things you'll need to follow the tutorial:

1. A working Python installation ([Anaconda](https://www.anaconda.com/products/individual) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html))
2. The SimPEG *conda environment* installed
3. A web browser that works with Jupyter
   (basically anything except Internet Explorer)

To get things setup, please do the following.

**If you have any trouble**, please ask for help in the
`t20-tue-simpeg` channel on the Software Underground slack.

**Windows users:** When you see "*terminal*" in the instructions,
this means the "*Anaconda Prompt*" program for you.

### Step 1: Python

**Follow the general instructions for Transform2020:** http://swu.ng/t20-python-setup
(there are also YouTube videos of [Windows](https://youtu.be/FdatS_NKVrM)
and [Linux](https://youtu.be/3ncwbHyZeAg))

This will get you a working Python 3 installation with the `conda` package
manager. If you already have one, you can skip this step.

### Step 2: Download the SimPEG tutorials

To access the notebooks, there are 3 options (in order of preference):
1. Use git to clone this repository
2. From GitHub, you can use the `download` option to download this repository as a zip file (follow all instructions below, replacing the `git clone` step with download and unzip the zip file with the repository contents.
3. You can run the notebooks online with binder through: https://mybinder.org/v2/gh/simpeg/transform-2020-simpeg/main

To clone this repository, open up a terminal and navigate to where you want this repository stored on your computer.

Then run
```
git clone https://github.com/simpeg/transform-2020-simpeg.git
```
to clone the repository, and `cd` into the `transform-2020-simpeg` directory
```
cd transform-2020-simpeg
```

### Step 3: Create the SimPEG tutorial conda environment

From inside of the `transform-2020-simpeg` repository, create the `t20-tue-simpeg` conda environment
```
conda env create -f environment.yml
```
and activate the environment
```
conda activate t20-tue-simpeg
```

### Step 4: Launching the notebooks

Once you have activated the conda environment, you can launch the notebooks
```
jupyter notebook
```
Jupyter will then launch in your web-browser.

If you are able to open any one of the notebooks and run the first cell, then you should be good to go!
If you run into issues, please post in the #t20-tue-simpeg slack channel.

## Resources

**Resources on Geophysics and Inversions**
- [Geophysics for Practicing Geoscientists](https://gpg.geosci.xyz/)
- [EM GeoSci](http://em.geosci.xyz/)
- Lectures from EOSC 350: Exploration & Environmental Geophysics ([2017](https://www.youtube.com/watch?v=C1U2okdfMbU&list=PLd9tNwsUm9jOhbLqjhjDW6ASqwRJtHTb5), [2018](https://www.youtube.com/watch?v=7kFPNooixyw&list=PLd9tNwsUm9jPrWrpdg1JHLieKrzK5w8_-))
- DISC 2017 lectures ([Mexico City](https://www.youtube.com/watch?v=uCnfWXWs5MM&list=PLd9tNwsUm9jM8GWLJm7XLLrE9PYuK-ca2))

**Resources on SimPEG**
- [Docs](http://docs.simpeg.xyz/)
- [Discourse](http://simpeg.discourse.group/)
- [Slack](http://slack.simpeg.xyz/)
- [This Tutorial](https://github.com/simpeg/transform-2020-tutorial/)


## License

All code and text in this repository is free software: you can redistribute it and/or
modify it under the terms of the MIT License.
A copy of this license is provided in [LICENSE](LICENSE).
