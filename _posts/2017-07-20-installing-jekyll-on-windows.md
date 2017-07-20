---
layout: post
title: Installing Jekyll on Windows
---
In which the intrepid developer describes the journey to get up-and-running with Jekyll development on Windows 10.
<!--more-->

## Jekyll: what, why, how
If you've been paying attention to trends in web development over the past few years, you've likely noticed the
 [movement toward static website generators](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/). 
 Makes sense, especially with a "mobile-first" motto, since static websites can be delivered much faster (among [other benefits](https://wsvincent.com/static-vs-dynamic-websites-pros-and-cons/)).
 
 [Jekyll](https://jekyllrb.com/) is one of the leading players in the static website generator arena. Without going into too much detail, Jekyll takes plaintext (Markdown) files, renders them through user-defined
 layout templates, and spits out static HTML files, with everything nicely linked together. One of the aspects that makes it especially appealing is that it is used by [GitHub Pages](https://pages.github.com/), which provides free personal 
 and project websites for GitHub users. This means that if you already have a GitHub account, you also already have a web host -- all you need to do is set it up.
 
## GitHub + Jekyll: starting out
 
 My journey to do just that started [with this article](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/), which describes how to get started with Jekyll and GitHub pages.
  This guide walks you through the (very easy) process of forking a starting repository to your own GitHub Pages site and customizing it from there. 
  In fact, you don't even have to install Jekyll (or anything else) locally at all -- GitHub Pages builds and serves the website for you, so you can simply push your unbuilt files to your repo as needed.
  
  *However*, if you are interested at all in developing your own theme (or any other major customization effort), you'll probably want to install Jekyll locally so that you can test your changes without having to push and wait
  for GitHub to build your site each time. If you're using a Mac or Linux, installing Jekyll is super-easy and there are already tons of guides addressing the [process](https://www.taniarascia.com/make-a-static-website-with-jekyll/) (so I won't).
  If you're using Windows... well, that's a different story entirely my friends!
  
## Where's my Windows `terminal`?
  Most of the guides written for [how to install Jekyll](http://jekyllrb.com/docs/installation/) (and all of its dependencies, such as Ruby) describe the command-line process used for Linux, Unix, or macOS.
  If you're stuck using Windows, we need to back up a bit first and get something that will provide us with a similar "terminal" install environment.
  
  The official docs for Jekyll include instructions for [installing Jekyll on Windows](http://jekyllrb.com/docs/windows/) but they are, frankly, a bit of a mess (and somewhat incomplete -- I couldn't get it working as written.)
  However, those instructions *did* point me toward the new [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about), which is *exactly* what's needed here -- an actual bash (Unix) terminal! Ideally, once we
  get that installed, we *should* be able to simply follow along with the Linux/Unix/macOS directions, rather than trying to cobble together a working system from VMs, emulators, and Windows-specific package managers.
  
  My recommendation if you're running Windows 10: ignore the official instructions linked above, and instead refer to the guides linked below.
  
  *(My recommendation if you're running Windows <10: upgrade to Windows 10.)*
  
## Installing Jekyll on Windows: step by step
  
  1. Follow the [Bash on Ubuntu on Windows installation guide](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide):
     - **Check your OS Build** and **Install the Windows Subsystem for Linux** (the first two steps).
     - If you don't want to sign up as a "Windows Insider", skip that section (I got things working without it)
     - Follow the next section to **Install using lxrun**.
     
  2. Follow [Dave Ruper's guide to install Jekyll](http://daverupert.com/2016/04/jekyll-on-windows-with-bash/) on Bash on Ubuntu on Windows.
  
  3. Browse to your site at [http://localhost:4000](http://localhost:4000). *(Optionally: Jump for Joy!)*
  
  4. If you run into errors when trying to `jekyll serve` locally, try one or more of the following:
  
     - If the error message includes the text `Failed to watch` and/or mentions something called `inotify`, you are likely suffering from the bug described at the top of the above guide. Try running either:
          - `jekyll serve --no-watch` or
          - `jekyll serve --force_polling`
     - For error messages which mention `bundler`, try running `bundle exec jekyll serve` (optionally with one of the flags above).
  
  5. That's the *minimum* necessary. If you want to use any Ruby gems (for plugins or other additional functionality), you'll likely have to install other packages as well.
     If you get errors when trying to `gem install` anything, check [Dave's guide to install Ruby](http://daverupert.com/2016/06/ruby-on-rails-on-bash-on-ubuntu-on-windows/) to see how to install some
     dependencies that you might be missing (typically the XML libs for Nokogiri).
     
  6. If you want, you can install the `github-pages` gem locally, to make sure that your local build environment matches GitHub's. The best way seems to be:
     - Install the Bundler package manager: `sudo gem install bundler`
     - Create (or edit) a `Gemfile` in your project directory and add the the following lines to it:
         ~~~~~~~~~~
         source 'https://rubygems.org'
         gem 'github-pages'
         ~~~~~~~~~~~~
     - Inside the directory containing the above Gemfile, run `sudo bundle install`.
     
  7. If you notice lots of 404's and/or lack of styling in your built site (whether before or after deploying to GitHub), be sure
     to read [Configuring Jekyll for User and Project GitHub Pages](http://downtothewire.io/2015/08/15/configuring-jekyll-for-user-and-project-github-pages/).
     It describes the correct way to set up your `_config.yml` and theme templates so that your site just **works**, whether locally or hosted, whether it's a GitHub user page or project page.


## Continuing the journey

I hope the guide was useful -- let me know! Also, check out the following additional resources:
  
  - [Jekyll docs](http://jekyllrb.com/docs/usage/) obviously... (With the exception of the install instructions for Windows, the Jekyll docs are actually pretty informative and straightforward.)
  
  - [Jekyll and GitHub tips for designers](https://michellehertzfeld.com/thoughts/using-jekyll-and-github-tips-for-designers/) -- Another "beginner" guide to Jekyll + GitHub
  
  - [Jekyll for GitHub setup on MacOS](https://www.taniarascia.com/make-a-static-website-with-jekyll/) in case you need it
      
  - [Add Teaser and Read-more Functionality](http://www.seanbuscay.com/blog/jekyll-teaser-pager-and-read-more/) to your templates.
  
  - [Add Reading Time to a post](https://medium.com/@r3id/jekyll-tips-tricks-315dd45eab0c)