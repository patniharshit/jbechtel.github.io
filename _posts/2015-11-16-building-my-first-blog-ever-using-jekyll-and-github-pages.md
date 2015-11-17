---
layout: post
title: Building my first blog ever using Jekyll and Github Pages
description: How I created my blog with no knowledge of html or css.
comments: True
tags: Jekyll Poole Github CSS HTML
---

## Origin Story

The decision to make my first blog stemmed from both a general feeling that all professionals these days maintain a strong web presence and the need for a creative outlet from grad school research. 

 In my head, I had an image of a professional-looking, streamlined website on a snazzy, custom domain like [jonathonbechtel.com](https://jonathonbechtel.com). Since I began this process with zero knowledge of `HTML` or `CSS`, I needed a service that provided highly templated but also highly customizable web pages. I thought I had found the holy grail with a Wordpress blog, and I quickly created an account, snatched up my custom domain name and chose a theme. But after an unreasonable number of frustrating **mouse clicks** navigating the page customization menus, I was already *fed up*. And when I realized that I wouldn't be able to write my posts in **Vim**, I frantically began searching for an alternative.  


## A Fresh Start
It was at this point that I found [Github Pages and Jekyll](https://pages.github.com/) along with a number of tutorials for customizing a Github-hosted personal website. A few key blogs helped ease the transition:

- [Joshua Lande's blog](http://joshualande.com/jekyll-github-pages-poole/) was an ideal jumping off point. This covers 
    - the basics of forking the [Poole](https://github.com/poole/poole), [Lanyon](https://github.com/poole/lanyon), or [Hyde](https://github.com/poole/hyde) (the basis of this blog) Github repositories.
    - adding an Archive, Disqus Comments, and Google Analytics support.
- [Kyle Stratis](http://kylestratis.com/2015/05/05/blog-setup-pt2/) provides in depth explanations for adding a Gravatar, custom Sidebar, and Tags page.
- [Patrick Steadman's blog](http://patricksteadman.ca/2014/08/04/lanyonsetup/) lists several customizations, and was credited by Kyle Stratis as inspiration for some of his tweaks. 
- [Lee Munroe's website](http://www.leemunroe.com/) also provided inspiration for my cool gradient color scheme.

But after completing the above tutorials I still wasn't completely satisfied with my layout. In order to get my site to its current state, I had to make some minor modifications which I outline below. 

## Local Build  
For some reason, the out-of-the-repo Hyde fork wouldn't compile locally with the `jekyll build` command. I saw this as a necessity for viewing my blog when drafting posts or when out of wifi range. In order to compile locally I had to comment out the  
{% highlight yaml %}
#relative_permalinks: true
{% endhighlight %}
line and add  
{% highlight yaml %}
gems: [jekyll-paginate, jekyll-gist]
{% endhighlight %}
after installing the gems on my machine. Now I can `jekyll serve` and `jekyll serve --drafts` with no issue. 

## Fancy Fonts
The default _Author_ font used on the sidebar isn't horrible, but I wanted to find something that I felt comfortable with. [Google Fonts](https://www.google.com/fonts) makes finding and implementing a new font incredibly simple. Head to the website, find a font that doesn't hurt your eyeballs, and click the right arrow "quick use" button. From there copy the `HTML` code   

{% highlight html %}
<link href='https://fonts.googleapis.com/css?family=Limelight' rel='stylesheet' type='text/css'>
{% endhighlight %}
and paste it in the `_layouts/head.html` file under the `<!-- CSS -->` section. Then open the `public/css/hyde.css` file and paste the Google Fonts `CSS` code into the appropriate section:


{% highlight css %}
/* About section */
.sidebar-about h1 {
  color: #fff;
  margin-top: 0;
  /*font-family: "Abril Fatface", serif;*/
  /*font-family: 'Monofett', cursive;*/
  /*font-family: 'Codystar', cursive;*/
  /*font-family: 'Faster One', cursive;*/
  /*font-family: 'Corben', cursive;*/
  font-family: 'Limelight', cursive;
  font-size: 2.25rem;
}
{% endhighlight %}

As you can see, I experimented with a few before I settled on Limelight.

## Hidden Sidebar Scroll Bar
I noticed when fidgeting around with my browser, that for abnormal display sizes, my sidebar would cut off content, with **no scroll bar**. This was annoying so I decided to change it. The [Poole/Hyde documentation]( https://github.com/poole/hyde) says that the sticky sidebar can be disabled by removing the "`.sidebar-sticky` class from the sidebar's `.container`", so I commented out the `.sidebar-sticky` part from `public/css/hyde.css` and also added `overflow-y: scroll` to the   
{% highlight css %}
@media (min-width: 48rem) {
  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 18rem;
    text-align: left;
    overflow-y: scroll;
  }
{% endhighlight %}
section. However, this is **not advised** because it added an _ugly, permanent_ scroll bar to my sidebar. To remedy this I decided to activate the scroll bar only upon a hover by the user's mouse. However this presented the unintended consequence of slightly shifting the sidebar width, along with the location of my Gravatar and Contact List, whenever I hovered over the sidebar. In order to address this, I added the hover attribute for the `.sidebar` class, and modified the `.sidebar-logo`, and `#contact-list` classes. The relevant code is 
{% highlight css %}
.sidebar {
  text-align: center;
  padding: 2rem 1rem;
  color: rgba(255,255,255,.5);
  background-color: #202020;
  overflow: hidden;
}

.sidebar-logo {
  padding-top: 5px;
  padding-bottom: 5px;
}

@media (min-width: 48rem) {
  .sidebar:hover {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 18.2rem;
    text-align: left;
    overflow-y: scroll;
  }
}

@media (min-width: 48rem) {
  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 18rem;
    text-align: left;
    overflow: hidden;
  }
  .sidebar-logo {
      float:left;
      padding-left: 20px;
      padding-top: 5px;
      padding-bottom: 5px;
    }
  #contact-list {
      float:left;
      padding-left: 50px;
      padding-top : -5px;
      padding-bottom: 5px;
    }
}
{% endhighlight %}
The `float:left` attribute is the key here; aligning everything prevents the jerkiness. Also, be careful not to define any conflicting style parameters in the `<div>` definitions in `_layouts/sidebar.html` 
{% highlight html %}
 <div class="sidebar-logo" >
      <img src="http://www.gravatar.com/avatar/{{ site.author.gravatar_md5 }}?s=200" />
  </div>
  <div style="clear: both;"></div>

  <div id="contact-list" style="font-size: 14px;">
  ...
{% endhighlight %}
At this point the scroll bar should cooperate at all browser sizes.
## Color Gradient
Hyde ships with eight color schemes based on [Chris Kempson's Base16 repo](https://github.com/chriskempson/base16), but I wanted something more eye-catching. With [Lee's site](http://www.leemunroe.com/) as my inspiration, I took the following steps to add a color gradient to the sidebar and to define a custom color scheme. It is possible to make a [variety of custom color gradients](https://css-tricks.com/css3-gradients/), but the easiest method I found was to choose a gradient from [uigradient.com](http://uigradients.com/#). Find a template that meets your _high aesthetic standards_, copy the `CSS` code and paste it at the bottom of `public/css/hyde.css` as so:
{% highlight css %}
/* Custom */
.theme-custom .sidebar {

  background: #1A2980 /* fallback for old browsers */
  background: -webkit-linear-gradient(120deg, #1A2980 , #26D0CE); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(120deg, #1A2980 , #26D0CE); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
.theme-custom .content a,
.theme-custom .related-posts li a:hover {
  color: #1A2980;
}
{% endhighlight %}
Here we have defined a custom theme `.theme-custom` that implements the color gradient with a 120 degree rotation. Also note that the last `color: #1A2980;` attribute is defined as the same color as the left-hand gradient color to maintain consistency. To actually use the custom color scheme open up `_layouts/default.html` and change the theme to custom:
{% highlight html %}
  <body class="theme-custom">
{% endhighlight %}

Voilà, you've created a tidy blog and a masterful visual experience using only a few lines of code.
