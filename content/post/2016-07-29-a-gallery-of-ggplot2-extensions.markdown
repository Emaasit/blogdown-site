---
title: A Gallery of ggplot2 Extensions
author: emaasit
date: 2016-07-29 02:58:44+00:00
categories:
  - Data Science
  - Data Visualization
  - ggplot2
  - R
slug: a-gallery-of-ggplot2-extensions
---

A couple of months ago, I announced the [ggplot2-extensions website](http://www.ggplot2-exts.org/) which tracks and lists extensions built on top of the popular R visualization package **[ggplot2](http://docs.ggplot2.org/current/)**.

Now, I wanted to make it even easier for R users to filter and search for these extensions and so I have added a [Gallery page](http://www.ggplot2-exts.org/gallery/). You can now search packages based on a filter like: if it's on CRAN; or if  it's for a particular task e.g. time series, networks, tech, etc.

![gallery](https://emaasit.files.wordpress.com/2016/07/gallery.png)

<!-- more -->

It's now easier for R developers to add their extensions to this Gallery. Submit a pull request by following these [simple instructions](https://github.com/ggplot2-exts/gallery#adding-a-ggplot2-extension):



	
  1. 


<blockquote>Fork the gallery [repository](https://github.com/ggplot2-exts/gallery) on Github.</blockquote>




	
  2. 


<blockquote>Create a png thumbnail of an interesting plot from your extension that will look good on a retina screen at 350x300 pixels and put this file in the `images` directory of [the gallery repository](https://github.com/ggplot2-exts/gallery).</blockquote>




	
  3. 


<blockquote>Add an entry for your extension in the `_config.yml` file of [the repository](https://github.com/ggplot2-exts/gallery) with the meta data for your extension.</blockquote>




	
  4. 


<blockquote>Push your changes and create a pull request.</blockquote>





**Acknowledgement**: Special thanks to [Dr. Ryan Hafen](http://ryanhafen.com/) ([@hafenstats](https://twitter.com/hafenstats)) for inspiring the design of this [Gallery page](http://www.ggplot2-exts.org/gallery/).


