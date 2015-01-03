---
layout: post
title: "Life as a GTK+ app developer"
date: 2015-01-04 07:09
comments: true
categories: [Meld]
---

The GTK+ 3 port of Meld was developed against 3.8, targetting 3.6. When I
started doing the port, 3.8 was what was available in current distributions,
so it seemed reasonable to expect that by the time the port was done, many
users would have access to it. In fact, it took way longer than I'd hoped and
the GTK+ 3 port was released at about the same time as GTK+ 3.14 came out,
which then broke everything.


GtkTextView/GtkSourceView painting
----------------------------------

Drawing in GtkTextView and GtkSourceView changed to use a new API involved
drawing of layers, and changed how the background was drawn. The new API is
actually really nice and will be great to use, but...

...well, it broke everything. The custom painting that Meld does all over the
textview was broken, and because the background clearing was a theme-specific
change, it broke differently in different themes.

Oh, and don't worry! All of this was completely unannounced. I found out about
the layer drawing by reading a random blog post *after* the release of 3.14
mentioning that it might be useful for another application. It will be too...
one day.


Images in dialogs
-----------------

Dialogs used to be guaranteed to have an image if a message-type was set. This
is no longer the case, so any code that assumed that there was going to be an
image there just breaks. Good job!

This broke lots of random dialogs in Meld, and prevented people from doing
things like... saving files.


Dialogs in general
------------------

Spacing, padding and outline drawing have all changed, so all our dialogs now
look awful. They'll have to be adjusted to look okay with GTK+ 3.14 which
will, by extension, make them look awful with everything pre-3.14.


Size calculation changes
------------------------

In 3.10, the way GtkBox expand properties propagate changed. Now granted, it
was weirdly broken before, but this behaviour change made a couple of bits of
Meld's preferences dialog unusable.


Life as a GTK+ app developer
============================

When Meld 3.12 was released, my plan was to get a really quick 3.14 release
done and out, and try for another quick release to sync up Meld and GNOME on
3.16. Instead, I've spent most of my very limited spare time plugging holes
in various regressions.

Accusations that level X of a technology stack doesn't really understand what
it's like for level Y of the technology stack aren't exactly new. Some vocal
members of the community will complain about this in any stack, and GTK+ is
no different. However, this is the first release cycle that I've spent hours
actively cursing breakages in the GTK+ stack. I hope it's a blip.

