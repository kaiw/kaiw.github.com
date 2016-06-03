---
layout: post
title: "Plucking a Mallard"
date: 2012-06-12 19:08
comments: true
categories: [Meld, Documentation]
---

Meld is in the process of getting nice new shiny
[Mallard](http://projectmallard.org/)-based documentation. There are several
things standing in the way of getting our new help actually distributed with
Meld --- not least of which being that I haven't yet pushed it to Git --- but
there's nothing much stopping me from making it available on the
[Meld website](http://meldmerge.org/).

Putting the Mallard docs online involved:

 * Formatting the docs as HTML
 * Pulling the necessary content out of the formatted docs
 * Fixing the Mallard-generated CSS to only apply to the embedded content


Mallard to HTML
---------------

While it's sadly not obvious that you can do this, you can use
`gnome-doc-utils` to
[generate fairly straightforward HTML and accompanying CSS](http://projectmallard.org/pipermail/mallard-list_projectmallard.org/2010-November/000037.html)
from Mallard documentation. 

    gnome-doc-tool css
    gnome-doc-tool html -c index.css --copy-graphics *.page

You'll get an HTML page for each Mallard page, and it'll all link to the
external CSS. No drama here.


Stripping the HTML
------------------

The HTML generated is designed to be stand-alone. However, we want to be able
to embed it in an existing webpage. Doing the simplest and hackiest thing
available, I used BeautifulSoup to just pull out the contents of the body, add
a header for Jekyll (Meld's site is hosted on GitHub) and rewrite the new
'HTML'.

I added a new Jekyll layout to be used for the help pages, and wrapped the
whole help content block in a `#help-content` `div`.


Massaging the CSS
-----------------

The generated CSS is all top-level rules and whatnot. Worse yet, it uses
*sensible* class names like "title", so you're bound to have conflicting
classes in an existing site. Again doing the stupidest thing that would work,
I wrapped the whole CSS file in:

    #help-content {
        ...
    }

and passed it through [Sass](http://sass-lang.com/) as SCSS. This stopped the
help CSS messing with the main site, but the help pages themselves were all
wrong due to some messy interaction with the existing CSS reset, etc. A few
additional (evil) styling overrides:

    #help-content {
      background-color: #ffffff;
    }

    #help-content div.body {
      border: none !important;
    }

    #help-content div.headbar {
      margin: 10px !important;
    }

    #help-content div.footbar {
      margin: 10px !important;
    }

    #help-content .title {
      line-height: 1em;
    }

    #help-content h1 {
      font-family: sans-serif;
      font-weight: bold;
      color: black;
    }

    #help-content h2 {
      font-family: sans-serif;
      color: black;
    }

and it looks pretty much like a sensibly-embedded Mallard page.

It's a pile of dirty hacks, but now at least Windows users can read our
documentation. [Check it out.](http://meldmerge.org/help/)

