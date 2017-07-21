---
layout: post
title: Jekyll Tips, Tricks, and Best Practices
---
Does what it says on the tin: an updated-as-I-discover-them collection of tips, tricks, etc. for Jekyll websites.
<!--more-->

## Jekyll: what's that again?
If you're just joining us (welcome!), you might not be familiar with the Jekyll static website generation engine.
[In its own words](http://jekyllrb.com/docs/home/):

> Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, 
> runs it through a converter (like Markdown) and our Liquid renderer, and spits out a complete, ready-to-publish static website suitable 
> for serving with your favorite web server. Jekyll also happens to be the engine behind GitHub Pages, which means you can use Jekyll to 
> host your project’s page, blog, or website from GitHub’s servers for free.

My recent adventures have involved setting up my personal GitHub page and
 [getting the Jekyll development environment set up on my Windows laptop]({{ site.baseurl }}{% post_url 2017-07-20-installing-jekyll-on-windows %}).
 Now that that's mostly sorted, we're moving on to the front-end stuff.
 
## The blessing and curse of Jekyll
Jekyll can be a bit two-faced *(much like its literary ~~namesake~~ eponym, methinks)*, in that one of the biggest benefits to Jekyll is also a huge drawback,
and that is the fact that it's so blank... open... unfettered... there are a multitude of different ways to configure and use it!

Which means there are a multitude of different problems that can happen, and a multitude of different solutions, and it can be
really, *really* hard to find a solution that works for your unique usecase. (Assuming you find a solution at all...)

To that end, I'm compiling-as-I-go a list of tips, tricks, solutions, and best practices that I've found to work for me. (YMMV)

Without further ado...

## The good stuff

### Getting Disqus comments working
Since Jekyll serves up static webpages, one must use third-party services for any dynamic content such as user comments. Disqus is one such service,
and [here's the steps I followed to get Disqus comments on my posts]({{ site.baseurl }}{% post_url 2017-07-21-setting-up-disqus-comments-on-jekyll %}).



## That's all for now...

Check back later -- I plan to add to this list as I find more useful tidbits.

Do you have a tip or trick you'd like to share? Leave your advice for your fellow Jekyll users in the comments below! :)

■