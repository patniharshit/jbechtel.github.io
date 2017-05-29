---
layout: post
title: Community Bonding Period (Week 3)
description: A summary of how I spent third week of community bonding period of GSoC 17
comments: True
tags: blog, community-bonding
---

## Third Week
###### (20/5 to 28/5)

Having read about colormaps and existing code I had got a fair idea of what is
needed to done. So I started planning for the coding period in the third week
and initiated discussion with mentors regarding how to approach the project.

* `Bivariate` colormap is more widely used term than 2D color maps
* It was decided that  2D/Bivariate will be in core library as a part of color
  and colorbar instead of existing as a standalone toolkit that lives under
  matplotlib repo.
* Any new class would subclass from existing colormap and norm because a lot of
  the underlying stuff is the same
* 2D normalizations that will work as independent 1D normalizations using
  existing normalizers on two variables

Testing those normalizers required ready-made 2D colormap. But I wasn't able to
find any ready-made look up tables for 2D colormaps on the internet So first
task became creating some colormaps by simply combining uniformly varying alpha
vector with an existing colormap in matplotlib.

```
def TwoDCM(gradient, alpha, cm):
    ret = cm(gradient)
    ret[:, 3] = alpha
    return ret
```

Resulting bivariate colormaps are shown below. These can be considered as
the prototype of my project too.

* Viridis
![viridis_bivariate](http://i.imgur.com/evlN286.png)

* Cool
![cool_bivariate](http://i.imgur.com/wPeWOKj.png)

* Plasma
![plasma_bivariate](http://i.imgur.com/OhzJGy8.png)