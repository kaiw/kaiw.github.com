---
layout: post
title: "Stored comparisons"
date: 2016-08-06 08:24
comments: true
categories: [Meld]
---

Meld has a rough time with showing recent comparisons. The fundamental problem
here is that toolkit support for recently-used files assumes that each entry
is a single file. I can't blame the toolkit for thinking this, since there's
probably less than a handful of cases where this isn't true, but since almost
all comparisons in Meld involve two or three files, it makes our life hard.


Hackety hack hack
-----------------

The hack that we have for this is to create fake `.meldcmp` files in the
user's data directory (e.g., `~/.local/share/meld/`) that contain a simple
description of the comparison, and then tell the recently used files API that
actually, this is the file the user opened. The files are in a pretty boring
format:

{% highlight ini %}
[Comparison]
type = File
paths = /home/foo/a.txt;/home/foo/b.txt
{% endhighlight %}

Meld knows how to recreate a comparison from one of these files, and to
support opening them from a desktop shell (which looks awful for completely
unrelated reasons) we accept them as command line parameters.


"Project" support
-----------------

One upshot of the above is that users can (ab)use this support to pre-define a
comparison and open it from the command line. Say that you saved the above
file into the `ab.meldcmp`, you could reopen this obviously vital comparison
with:

{% highlight shell %}
meld --comparison-file=ab.meldcmp
{% endhighlight %}

While we currently don't support anything more exciting, there's nothing
stopping us from adding more "project" style setup to these files... you know,
other than fear of complexity and feature creep.
