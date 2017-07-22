---
layout: post
title: Setting Up Disqus Comments on Jekyll
---
Part of an ongoing-as-I-discover-them series featuring a collection of tips, tricks, etc. for Jekyll websites.
In today's episode we discuss Disqus.
<!--more-->

{% include jekyll-shpiel.html %}

## Getting Disqus comments working
Since Jekyll serves up static webpages, one must use third-party services for any dynamic content such as user comments. Disqus is one such service,
and here's the steps I followed to get Disqus comments on my posts.

1. Sign up at [Disqus](https://disqus.com/), enter your details. They will provide you with a "**shortname**", keep this handy.

2. In your `_config.yml` file, add (or edit) the following key:
   ~~~~~ yaml
     disqus:
       shortname:  # Here's where you put your unique shortname
   ~~~~~ 

3. Create a new file in your `_includes` folder called `disqus.html`. In that file goes:
   ~~~~~ html
    {% raw %}
    <!-- Disqus comments section goes here (if comments are enabled) -->
    {% if page.comments == true and jekyll.environment == "production" %}
     
    <div class="comments">
    <div id="disqus_thread"></div>
     
    <script type="text/javascript">
     
    /* * * STOP! * * */
    /* You shouldn't need to edit ANYTHING below to get this working! */
    /* Instead, edit the key `disqus.shortname` in _config.yml */
     
    var disqus_config = function (){
    this.page.url = '{{ page.url | absolute_url }}';
    this.page.identifier = '{{ page.url }}';
    };
     
    (function() {
    var d = document, s = d.createElement('script');
    s.type = 'text/javascript'; s.async = true;
    s.src = 'https://{{ site.disqus.shortname }}.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
    
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    </div>
     
    {% endif %}
    {% endraw %}
   ~~~~~ 
   As per the warning, you shouldn't need to edit anything in this section; simply setting your Disqus shortname in your config file should do the trick.

4. For every page type on which you want a comments section, edit the corresponding layout file -- typically this will be `_layouts/post.html`.  
   Add in the following bit of logic in the appropriate area in the layout file:
   ~~~~~ html
     {% raw %}
     {% if page.comments == true and site.disqus.shortname %}
       {% include disqus.html %}
     {% endif %}
     {% endraw %}
   ~~~~~ 
   
5. Note that both of the above blocks of code will only render if `page.comments == true`. This is a failsafe, since you might not want comments on
   each and every post all the time. You can set the value to "true" in one of two ways:
   
   - In the Front Matter of each blog post, simply include the setting `comments: true`.
   
   - If you want to default to comments being enabled for all blog posts, include the following lines in your `_config.yml`:
     ~~~~~ yaml
       defaults:
         -
           scope:
             path: ""
             type: "posts"
           values:
             layout: "post"
             comments: true   # change to false to default to comments off site-wide
     ~~~~~ 
     This will set the default value `comments: true` for all posts, site-wide. You can then disable comments on an individual post by
     simply setting `comments: false` in its front matter.
     
     
6. Finally, go to your Admin panel on the Disqus site and double-check the Settings for your site. You may need to tweak some things in order
   to get it working, and unfortunately, it may take some time for the changes to propagate.
   
   *In particular,* if you're hosting a GitHub User page, with a domain of the format `http://YOU.github.io`, 
   you might need to change your Website URL in the Disqus Settings to:
   ~~~~~~
     http://YOU.github.io/YOU.github.io
   ~~~~~~
   ... since that is the actual name of the subfolder your website is in (GitHub just redirects to the subdomain, from what I understand).
   
   Also note that **you won't be able to see comments when developing locally** -- you need to `git push` and wait for your site to build on GitHub.
   (And also possibly wait for Disqus to update with any changes you've made.)
   


I hope this was helpful -- let me know in the comments below (hopefully mine are still working!)
And as always, thanks for reading! :)

■