---
layout:  post
title: "A Tidyverse Style Guide"
comments:  true
published:  true
author: "Yeedle"
date: "2017-01-15 09:50:00 EDT"
categories: [R, tidyverse, "style guide"]
output:
  html_document:
    mathjax:  default
    fig_caption:  true
    highlight: haddock
excerpt: "How to style your code, when you code with the tidyverse"
---

<style>
div.bad > figure.highlight > pre { background-color:rgba(255, 0, 0, 0.2); }
div.good > figure.highlight > pre { background-color:rgba(0, 255, 0, 0.2); }
</style>


The two most popular [^citationeeded] R style guides are the [Google's R Style Guide](https://google.github.io/styleguide/Rguide.xml) and [Hadley Wickham's Style Guide](http://adv-r.had.co.nz/Style.html). But these guides only address base R code. The Tidyverse comes with its own set of conventions. The following is an attempt at organizing the coding conventions for the Tidyverse.

[^citationeeded]: [[<u>Citation needed</u>]](https://xkcd.com/285/)

# General Script Structure

### Pacakge Declarations
If you're using several Tidyverse pacakges, use `library(tidyverse)` instead of listing them all individually.

### Line Length
Many style guides mention to never let a line go past 80 (or 120) characters. If you're using RStudio, there's a helpful setting for this. Go to Tools -> Global Options... -> Code -> Display, and select the option "Show margin", and set "margin column" to 80 (or 120).

When arguments to functions overrun the 80 character limit, break them up into multiple lines and use spaces to align them. This applies in particular to pipes where multiple levels of indentation can quickly lead to overflowing lines.

# Pipelines

Each step in a pipeline should be on its own line, even for for short pipes.
<div class = "good">
GOOD:

{% highlight r %}
mtcars %>% 
  mutate(cyl = cyl * 2) %>%
  mutate(mpg = mpg + 2)
{% endhighlight %}
</div>

<div class = "bad">
BAD:

{% highlight r %}
mtcars %>% mutate(cyl = cyl * 2) %>% mutate(mpg = mpg + 2)
{% endhighlight %}
</div>

Every line past the first line should be indented with two spaces.
<div class = "good">
GOOD:

{% highlight r %}
mtcars2 <- mtcars %>%
  mutate(cyl = cyl * 2) %>%
  group_by(gear) %>%
  summarise(avg_disp = mean(disp))
{% endhighlight %}
</div>

<div class = "bad">
BAD:

{% highlight r %}
mtcars2 <- mtcars %>% 
mutate(cyl = cyl * 2) %>%
group_by(gear) %>%
summarise(avg_disp = mean(disp))
{% endhighlight %}
</div>


Keep your pipelines under ten pipes. If your pipeline is longer than that, break up the pipline into intermediate objects with meaningful names [^tenperpipeline]

[^tenperpipeline]:[Wickham, 2017](http://r4ds.had.co.nz/pipes.html#when-not-to-use-the-pipe)

When breaking up a pipe into multiple intermediate objects, don't use the same name with a suffix attached (e.g. `foo_1`, `foo_2`, etc.), rather try to come up with a meaningful name that summarizes the pipe's goal (e.g. `foo_summarized_by_bar`).

<center>
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/davidjayharris">@davidjayharris</a> <a href="https://twitter.com/ucfagls">@ucfagls</a> yeah that often trips me up. Accidentally run same line twice and end up in weird state</p>&mdash; Hadley Wickham (@hadleywickham) <a href="https://twitter.com/hadleywickham/status/819202162211385347">January 11, 2017</a></blockquote>
<script async src="http://platform.twitter.com/widgets.js" charset="utf-8"></script>
</center>

Avoid the assignment operator `%<>%` whenever possible (which is to say, always).[^%<>%] Instead, use explicit assignment. Also, don't use the `->` assignment operator at the end of a pipe.

<div class = "good">
GOOD:

{% highlight r %}
mtcars <- mtcars %>% 
  group_by(gear) %>%
  summarise(avg_disp = mean(disp))
{% endhighlight %}
</div>

<div class = "bad">
BAD:

{% highlight r %}
mtcars %<>% 
  group_by(gear) %>%
  summarise(avg_disp = mean(disp))
{% endhighlight %}
</div>

<div class = "bad">
BAD:

{% highlight r %}
mtcars %>%
  group_by(gear) %>%
  summarise(avg_disp = mean(disp)) -> mtcars
{% endhighlight %}
