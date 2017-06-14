---
layout: post
title: Coding Period Starts!
description: Update on work done in week 1 and week 2 of coding period
comments: True
tags: blog
---

## First Week

After creating a basic bivariate colormap in end of community bonding period, next 
task was to map some structured data with that map. It was quite easy to do but I
was doing it in a wrong way and it took 3-4 days without any results. It was then
decided to move on from that task since supporting code to plot data with bivariate
colormaps was not there.

Then for couple of days I wrote code for  `BivariateNorm` which naively uses two
instances of `matplotlib.colors.Normalize` and outputs correspondingly normed variables.
Although this `BivariateNorm` doesn't do anything new but it will be required for
plotting functions like imshow, pcolormesh, scalar mappables etc so that the bivariate
mapping can be integrated in matplotlib similar to the univariate mapping. The PR is
open and has been reviewed once by mentors but has been marked as `WIP` i.e. work in
progress because there is no point in merged `BivariateNorm` till any support for
bivariate mapping comes up in matplotlib which will be coming in upcoming weeks.


## Second Week

My mentor pointed me to some research papers related to bivariated/multivariate mappings
shared on a [blog](http://graphics.cs.wisc.edu/WP/vis10/archives/998-reading-9-bi-variate-color-mappings) 
of some data visualization class. I started reading four of them and by far I have completed
reading three.

### [Quantitative Texton Sequences for Legible Bivariate Maps, Colin Ware](http://ieeexplore.ieee.org/document/5290769/?tp=&arnumber=5290769)
This paper dwells into an interesting way to map the second variable to a `QtonS` or
in simple language some kind of sequence of glyphs instead of alpha which is what I have been doing.

![qtons](https://www.computer.org/cms/Computer.org/dl/trans/tg/2009/06/figures/ttg20090615232c.gif)

### Rheingans, Task-based Color Scale Design In Proceedings Applied Image and Pattern Recognition
This paper listed, classified and considered pros and cons of various types of colormaps
suiting for different tasks.

### [Daniel A. Keim, “Designing Pixel-Oriented Visualization Techniques: Theory and Applications](http://fusion.cs.uni-magdeburg.de/pubs/TVCG00.pdf)
This paper gave me a new idea to improve upon what the static bivariate map. This involves
creating a bivariate colormap as a weighted average of two univariate colormaps and then
providing a physical knob to user to slide to change the weight of different univariates 
in bivariate map. Keeping slider on extremes will simply produce univariate maps. This
gives total independence to user to analyze the different variables combined as well as 
seperately. So if any features of a variables are hidden or lost in bivariate mapping then
user can simply observe the variable independently without having to plot it seprately. 
Lets see how things work out with project timeline, I would definitly like to see this
feature added on top of what I have promised as GSoC project if time permits.


#### Plot of some structured data with bivariate colormap

Also finally out of blue I figured out how to plot mapped colors with imshow.
Although this isn't perfect, just couple of hacks but this is quite close to what
end product of project will look like.

* Here to plot with bivariate I have used height of sinc function (sin(R)/R where
  R = sqrt(X^2 + Y^2) as one variable and gradient of sinc with respect
to X as second variable
* Second variable is mapped to alpha and first variable to 1D colormap

![sinc_bivariate](http://i.imgur.com/439dUH8.png)
