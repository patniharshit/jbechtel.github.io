---
layout: post
title: Community Bonding Period (Week 2)
description: A summary of how I spent second week of community bonding period of GSoC 17
comments: True
tags: Blog
---

## Second Week
###### (12/5 to 19/5)

This week mentor suggested me to go through the existing colormap code in
Matplotlib. New classes for 2D Colormaps will also be developed on similar
lines and in some case will inherit from them.

* Went through cm.py, colors.py. Trying to understand how 1D normalizations
  works, how user data is mapped to a colormap etc
* Halfway through colorbar.py
* Converted `colorbar_only` example in matplotlib gallery into a tutorial
  [#8600](https://github.com/matplotlib/matplotlib/pull/8600)
* Fixed an issue by adding test for `_num_to_string` method used in `__call__`
  of `LogFormatter` [#8598](https://github.com/matplotlib/matplotlib/pull/8598)
* Debugged failing tests because of segmentation fault in qt backend