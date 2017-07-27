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
Jekyll can be a bit two-faced *(much like its literary ~~namesake~~ eponym)*, in that one of the biggest benefits to Jekyll is also a huge drawback,
and that is the fact that it's so blank... open... unfettered... there are a multitude of different ways to configure and use it!

Which means there are a multitude of different problems that can happen, and a multitude of different solutions, and it can be
really, *really* hard to find a solution that works for your unique usecase. (Assuming you find a solution at all...)

To that end, I'm compiling-as-I-go a list of tips, tricks, solutions, and best practices that I've found to work for me. (YMMV)

Without further ado...

## The good stuff

### Getting Disqus comments working
Since Jekyll serves up static webpages, one must use third-party services for any dynamic content such as user comments. Disqus is one such service,
and [here's the steps I followed to get Disqus comments on my posts]({{ site.baseurl }}{% post_url 2017-07-21-setting-up-disqus-comments-on-jekyll %}).

### Using _data for things like social media
Following the 'DRY' development principle, it makes the most sense to define anything -- especially a collection of data -- only once, and utilize a `for` loop to display it as needed. This works really well for [including a series of linked social media icons on your Jekyll site]({{ site.baseurl }}{% post_url 2017-07-25-social-media-icons-on-jekyll %}).

### Setting per-post (or per-page) custom CSS
Helps you [manage your CSS styles]({{ site.baseurl }}{% post_url 2017-07-26-per-page-custom-css-in-jekyll %}) (and JS files) so that only the posts that need'em, get'em.


## That's all for now...

Check back later -- I plan to add to this list as I find more useful tidbits.

Also check out my collection of [Bookmarks]({{ site.baseurl }}{% link _pages/bookmarks.md %}) for more valuable resources!

Do you have a tip or trick you'd like to share? Leave your advice for your fellow Jekyll users in the comments below! :)

■

*[DRY]: Don't Repeat Yourself
