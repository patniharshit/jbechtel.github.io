---
layout: post
title: Bivariate mapping integrated to plotting
description: Update on work done in week 5 and week 6 of coding period
comments: True
tags: blog
---

After the first month, I  started to integrate bivariate mapping to matplotlib's
plotting functions like `imshow`, `pcolor`, `pcolormesh`, 'pcolorfast` and
`scatter`. The main challenge was modifying matplotlib's current mechanism
which assumes 2d arrays are to be mapped with colormap and 3d array having
shape that of RGB and RGBA arrays are to be plotted as is. So after some
discussion with mentors we decided instead of changing matplotlib's current
code in several places like `_image.resample` it will be much easier if we
tackle this problem on our side by changing our current approach which
maintains the two dimensions of bivariate data.

My mentor Hannah then came up with an idea to map bivariate data to some
univariate and then mapping it to 2d colormap by flattening the 2d colormap
to 1d look up table. This way by just modifying the incoming data we can
get around the hassle of modifying the matplotlib's code in a lot of places.

So finally I modified the before mentioned plotting functions as planned and
then plotted some temperature and pressure data with some made-up bivariate
colormap which is nowhere near good but serves the purpose.

In the coming weeks, there will be more work on the bivariate colormap. But
next on my todo list is the 2d colorbar or color square.

![bivaraite-plotting](http://i.imgur.com/fuvpRwM.png)
