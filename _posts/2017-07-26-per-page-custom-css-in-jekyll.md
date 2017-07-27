---
layout: post
title: Setting Per-Page Custom CSS in Jekyll
---
This article is part of a collection of tips, tricks, etc. for Jekyll websites. Today's lesson: how to set a custom CSS for each page or post!
<!--more-->

{% include jekyll-shpiel.html %}

## Cascading Styles -- just like it's meant to!

The reasoning behind why you might want to set a different CSS (or JavaScript) on different posts/pages is explained in this blog post: [Page-specific assets with Jekyll](http://mattgemmell.com/page-specific-assets-with-jekyll/), and the instructions are pretty much adapted from there, as well.

But, as an example, let's say that you decide to put your resume / CV on your Jekyll site, and perhaps you want it to be typographically styled just a bit differently than the rest of your website. Easy to do!

In the Front Matter of the page, include a custom variable like so:

~~~~~ yaml
layout: page
title: My Awesome Resume!
custom_css: resume
~~~~~

Then, in whatever file in contains the code for the &lt;HEAD&gt; section of your HTML document (good candidates are `_layouts/default.html` or `_includes/head.html`), insert the following AFTER any other CSS declarations:

~~~~~ html
{% raw %}
  {% if page.custom_css %}
    {% for stylesheet in page.custom_css %}
    <link rel="stylesheet" href="{{ site.baseurl }}/assets/css/{{ stylesheet }}.css">
    {% endfor %}
  {% endif %}
{% endraw %}
~~~~~

Adjust the `/assets/css/` in the href to correspond to whichever directory you keep all your CSS files.

Finally, create your new stylesheet, named `resume.css` in this case (and saved to the above folder).

## You can add custom JavaScript too!

This is also a dead-simple way to include a script in the HEAD section of an individual page. Again, add a custom variable (or list of variables, in this case) to the page's Front Matter:

~~~~~ yaml
layout: page
title: My Awesome Portfolio!
custom_js:
- awesome-project-demo
- another-great-demo
~~~~~

Now, in that same file with the &lt;HEAD&gt; section, insert the following (again, after any existing script tags):

~~~~~ html
{% raw %}
  {% if page.custom_js %}
    {% for js_file in page.custom_js %}
    <script type="text/javascript" src="{{ site.baseurl }}/assets/js/{{ js_file }}.js"></script>
    {% endfor %}
  {% endif %}
{% endraw %}
~~~~~

As before: adjust the path in the `src`, make your files, and you're good to go!


That's it! It's really one of the easiest, and most useful, Jekyll hacks I've found to date. Thanks to the original blog author [Matt Gemmell](http://mattgemmell.com/page-specific-assets-with-jekyll/), and thank *you* for reading! :)
■