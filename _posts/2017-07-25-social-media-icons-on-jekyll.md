---
layout: post
title: Including Social Media Icons on Jekyll through the use of Data Files
---
Part of an ongoing series featuring a collection of tips, tricks, etc. for Jekyll websites. Here we dive into _data files and use them to render a series of social media buttons.
<!--more-->

{% include jekyll-shpiel.html %}

## Social media icons, the repetitive (wrong) way
I've seen at least one Jekyll theme that displays social media icons by asking the user to
define their social media handles in _config.yml, and then it checks each.and.every.one via separate `if` statements. For instance:

~~~~~ html
{% raw %}
<div id="socialMedia">
{% if site.social-media.email %}
    <a href="mailto:{{ site.social-media.email }}" title="Email"><i class="fa fa-envelope-square"></i></a>
{% endif %}
{% if site.social-media.facebook %}
    <a href="https://www.facebook.com/{{ site.social-media.facebook }}" title="Facebook"><i class="fa fa-facebook-square"></i></a>
{% endif %}
{% if site.social-media.twitter %}
    <a href="https://www.twitter.com/{{ site.social-media.twitter }}" title="Twitter"><i class="fa fa-twitter-square"></i></a>
{% endif %}
.
.
.

</div>
{% endraw %}
~~~~~

This is a *terrible* way to do things, for a few reasons:
- Look at all those repeated `if` statements! There's *got* to be a better way...
- If we ever need to change anything, it's a lot to scan through.
- If we want to use any of this data in a slightly-different form elsewhere, we'll likely need to write out much of this stuff (`href`, `title`, etc.) all over again.


## Storing social media information in _data
Instead, let's use Jekyll's built-in **data** ability for its intended purpose. In your project's root directory, make a new folder called `_data`. Inside this folder, make a new file called `social-media.yml`, containing the following:

~~~~~ yaml
email:
  id: 'your.name@yoursite.com'
  href: 'mailto:'
  title: 'Email'
  fa-icon: 'fa-envelope-square'

facebook:
  id: 'your-facebook-username'
  href: 'https://www.facebook.com/'
  title: 'Facebook'
  fa-icon: 'fa-facebook-square'

twitter:
  id: 'your-twitter-name'
  href: 'https://www.twitter.com/'
  title: 'Twitter'
  fa-icon: 'fa-twitter-square'

github:
  id: 'your-github-name'
  href: 'https://github.com/'
  title: 'GitHub'
  fa-icon: 'fa-github-square'
~~~~~

(It's really up to you how you want to format your data. Jekyll provides support for YML, JSON, and CSV data formats.)

## Displaying the data via a loop
Given that you've created some data using the above format, you can loop through the data to display it on your site. In your `_includes` folder, create a file called (for example) `social-media-links.html` with the following code:

~~~~~ html
{% raw %}
{% if site.data.social-media %}
<div id="social-media">
    {% assign sm = site.data.social-media %}
    {% for entry in sm %}
        {% assign key = entry | first %}
        {% if sm[key].id %}
            <a href="{{ sm[key].href }}{{ sm[key].id }}" title="{{ sm[key].title }}"><i class="fa {{ sm[key].fa-icon }}"></i></a>
        {% endif %}
    {% endfor %}
</div>
{% endif %}
{% endraw %}
~~~~~

This code first checks to see if we have a data file called `social-media`. If so, we assign it to the shorter variable `sm`, and loop through each `entry`. We capture the first part of each entry (the `key`) and use that to reference each bit of our social media data. For each key with an `id` value defined in the data file, Jekyll will render the link and the icon. Here's some sample output, using the `facebook` data entry:

~~~~~ html
<a href="https://www.facebook.com/your-facebook-username" title="Facebook"><i class="fa fa-facebook-square"></i></a>
~~~~~

And it renders like so: <a href="https://www.facebook.com/thereeljess" title="Facebook"><i class="fa fa-facebook-square"></i></a>

## Usage notes
- Include the output on your site via the `{% raw %}{% include social-media-links.html %}{% endraw %}` tag.

- Note that because the above code checks that the `id` exists, you can opt to leave some entries blank in the data file to fill in later, or create a theme and let the end user fill it in, or whatever.

- The class `fa-icon` requires the [FontAwesome](http://fontawesome.io/) stylesheet to be included on your site.

- Now that you've defined everything once already, you can easily add a link to (for example) your email address on any other page:
  ~~~~~ html
  {% raw %}
  <a href="{{ site.data.social-media.email.href }}{{ site.data.social-media.email.id }}" title="Email me">Click here to send me an email!</a>
  {% endraw %}
  ~~~~~

  (This becomes even better when you realize that if you do things this way, you only have to replace a single entry in the data file if your email address ever changes!)

I hope that this gives you other ideas on how to use Jekyll data to improve your own website -- share your ideas in the comments below. Thanks for reading! :)

■