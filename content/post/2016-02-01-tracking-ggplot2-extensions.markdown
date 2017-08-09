---
title: Tracking ggplot2 Extensions
author: emaasit
date: 2016-02-01 23:55:06+00:00
categories:
  - Data Science
  - Data Visualization
  - R
slug: tracking-ggplot2-extensions
---

![ggplot2-2](https://emaasit.files.wordpress.com/2016/02/ggplot2-2.png)


### **Introduction**


The purpose of this blog post is to inform R users of a [website](http://ggplot2-exts.github.io/index.html) that I created to track and list **ggplot2 extensions**. The site is available at: [http://ggplot2-exts.github.io](http://ggplot2-exts.github.io). The purpose of this site is to help other R users easily find [ggplot2](http://ggplot2.org/) extensions that are coming in "fast and furious" from the R community.

If you have developed or intend on developing ggplot2 extensions, submit them so that other R users can easily find them. To do so, simply create an issue or a pull request on this [github](https://github.com/ggplot2-exts/ggplot2-exts.github.io/tree/dev) repository.

Incase you are wondering what ggplot2 extensions are; these are R packages that extend the functionality of the [ggplot2 package](http://ggplot2.org/) by [Dr. Hadley Wickham](http://had.co.nz/). This extensibility mechanism became available in ggplot2 version 2.0.0 [released on December 17th, 2015](http://blog.rstudio.org/2015/12/21/ggplot2-2-0-0/).

<!-- more -->


### **Motivation for Developing this Website**


When Hadley announced the release of ggplot2 2.0.0, perhaps the most exciting news was the addition of an official extension mechanism. This mechanism allows other R developers to easily create their on stats, geoms and positions, and provide them in other packages. This means that even when less development occurs in the ggplot2 package itself, the community will continue to release packages for graphical analysis that extend/solve different requirements. (To learn how you can develop your own extensions, there's a step by step tutorial here: [https://cran.r-project.org/web/packages/ggplot2/vignettes/extending-ggplot2.html](https://cran.r-project.org/web/packages/ggplot2/vignettes/extending-ggplot2.html))

Immediately after this announcement, several extensions started popping up. I was able to learn of some because they were posted out on twitter by [@hadleywickham](https://twitter.com/hadleywickham).

![Screenshot_2016-01-30-10-52-46-1](https://emaasit.files.wordpress.com/2016/02/screenshot_2016-01-30-10-52-46-1.png?w=680)

But it got me thinking..... R users who are not active on social media must be missing out on these new cool extensions. In addition, if I didn't check my twitter feed on a particular day, I would miss tweets about new extension-packages. This was not an effective way of searching for packages. There has to be a better way to track and list ggplot2 extensions. Quickly, I sprang into action to help fill this gap. But first, I had to find out if such an initiative already existed in the R community.

![Screenshot_2016-01-30-10-52-27-1](https://emaasit.files.wordpress.com/2016/02/screenshot_2016-01-30-10-52-27-1.png?w=680)

It turned out none existed. I quickly started developing one and a couple of hours later, we had a working website ([http://ggplot2-exts.github.io](http://ggplot2-exts.github.io/)) with a list of extensions known to me then.

![ggplot2-3](https://emaasit.files.wordpress.com/2016/02/ggplot2-3.png)

Hadley was kind enough to inform his followers on twitter about this new initiative. (I should mention, it was the highlight of my life getting a "thumps up" from Hadley Wickham).

![Screenshot_2016-02-01-15-12-16-1](https://emaasit.files.wordpress.com/2016/02/screenshot_2016-02-01-15-12-16-1.png?w=680)

As it turns out, I was not the only one concerned about this issue. Several other R users had made similar inquiries.

![Screenshot_2016-01-30-10-49-14-2](https://emaasit.files.wordpress.com/2016/02/screenshot_2016-01-30-10-49-14-2.png)


### **Closing Remarks**


In closing, I hope to see more cool extensions being developed and shared with the rest of the community on [ggplot2-exts.github.io](http://ggplot2-exts.github.io) so that other R Users can easily find them. Don't forget to create an issue or a pull request on this [github](https://github.com/ggplot2-exts/ggplot2-exts.github.io/tree/dev) repo.
