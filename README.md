# Jekyll-Relative-Bootstrap

Jekyll from Server to File Manager to Dropbox - Relative Links, Relative URI's

## Usage & History

For all usage and documentation please see: <http://jekyllbootstrap.com>, this is just a fork of that project.

It started with this Stack Overflow question: <http://stackoverflow.com/questions/7985081/how-to-deploy-a-jekyll-site-locally-with-css-js-and-background-images-included>

I wanted a way to host a website on a shared network folder at work.  This is the result of that.  Please fork, issue requests and do whatever you can to improve this.  It is just a start.

## Purpose

The files generated can be hosted on a web server, on a local folder or in your Dropbox Public folder.  The dropbox folder acted funny with some of the link sharing, and that is why there are extra slashes in paths.  It would be nice to eliminate these slashes at some point.

## Methods of Retaining Relative URL's throughout

As taken from the Stack Overflow question mentioned above.  Three methods were used.

  1 - YAML Headmatter indicating the root.  This YAML headmatter is later called upon in liquid templates.  For example:

        ---
        layout: page
        title: Relative Bootstrap
        root: .//
        ---
  
  2 - Liquid templating code that saves and calls the root wherever you are.  This is done by creating a file and then calling that file wherever necessary.  The file is named 'root' and located in '_includes'  its contents are:

	    {% capture root %}{% if page.root %}{{ page.root }}{% else %}{{ post.root }}{% endif %}{%endcapture%}

This file is then called upon at the beginning of a page, layout, partial or helper like this:

    {% include root %}

Then the 'root' include can be used anywhere for example as found in 'index.md':

    <a href="{{ root }}{{ post.url }}">{{ post.title }}</a></li>  
  
  3 -  A third file for CSS stylesheets is also created and located in '_includes'.  It is named 'relativecss'  its contents are:

        {% capture root %}{% if page.root %}{{ page.root }}{% else %}{{ post.root }}{% endif %}{%endcapture%}

    <!-- Le styles -->
      <link href="{{ root }}{{ ASSET_PATH }}/css/1.4.0/bootstrap.css" rel="stylesheet">
      <link href="{{ root }}{{ ASSET_PATH }}/css/style.css?body=1" rel="stylesheet" type="text/css" media="all">

It is then called upon in this manner on the base html layout:

    {% include relativecss %}
  
Thats a quick summary of what was done to modify the jekyll-bootstrap and make it relative pathed throughout.

## Problem

I cannot figure out how to preserve the relative links and not have trailing slashes.  Every time I get red of the trailing slashes by modifying the YAML head matter, the site won't load without a web server.

As an example this is what happens as the site is browsed:

http://originalsurfmex.github.com/jekyll-relative-bootstrap///////////////////////index.html

Any help in this would be much appreciated!
  

## Other Projects

Middleman is a great static website generator, however getting it to do this was too tricky and inconsistent.

Webby and Webgen do this but they have not been updated for a couple of years.

Pith does this very nicely, however it has no instructions to push to Heroku, and I could not find examples of other sites that have been built with it besides that of the programmer.

Sphinx Document Generator does this awesomely, however it is not as elegant to theme and design with.  That being said, Sphinx is incredible.

Nesta CMS is powerful and can probably do this statically, however it doesnt have a good twitter bootstrap theme yet.

If you have any suggestions for other projects that would accomplish this better please let me know.

## License

[Creative Commons](http://creativecommons.org/licenses/by-nc-sa/3.0/)