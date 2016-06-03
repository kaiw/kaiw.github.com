---
layout: post
title: "Things that suck about Meld that I learned about by writing user help"
date: 2012-06-28 06:52
comments: true
categories: [Meld, Documentation]
---

In any software that you work on, there are always pain points; there are
things that you *know* aren't great, but are low priority or hard to fix or
would mean changing established behaviours. It's when you sit down to document
how these things work that you realise *just how much these things suck*.

If developers had to document the bizarre corners of their UI, I'm sure we'd
have far fewer bizarre corners. By way of example, while writing
<a href="http://meldmerge.org">Meld's</a> new help docs, I simply couldn't
bring myself to write the sentence "Toggle a case insensitive comparison by
clicking 'Case' on the toolbar", so ended up rearranging the toolbar and fixing
some labels. The world is better for it.

The following is a very incomplete list of the things that made me feel ashamed
when documentating them.


Which file gets saved?
----------------------

When you "Save", Meld only saves the currently focussed file. This is mostly
sensible; the other option would be to save all files in the current
comparison, which is often *not* what you want.

However, this means explaining that we only save one file, and that's the
'focussed' file. What's a focussed file? Oh, that's the one that your cursor is
currently in. What do you mean you can't see the cursor? It's that tiny
one-pixel wide vertical bar in the... oh, right. Look, the focussed file is
the last one you were editing... probably.

Actually, you know what? Forget it.

I'm sorry.


Why are your shortcuts all different?
-------------------------------------

A while ago I fixed a long-standing request to be able to switch panes in
file comparisons using the keyboard. Turns out I didn't bother to apply the
same method to folder comparisons, even though it's *much* easier to do.
Admittedly, adding this would mean that there were two ways of switching
panes in directory comparisons, but at least one of those ways would be
consistent across different comparison types.

I'll [fix this](https://bugzilla.gnome.org/show_bug.cgi?id=679007) eventually.


View » Hide? Case? What?
-------------------------

The menu item to toggle case-insensitive comparison was labelled "Case",
probably so that it would fit on the toolbar... but it's not important enough
to warrant being on the toolbar anyway.
[Fixed](http://git.gnome.org/browse/meld/commit/?id=3b24e07f65e8d5bd561c4925a487e15a64ce941a)
and [fixed](http://git.gnome.org/browse/meld/commit/?id=6709339af6478e3576f3a76e35f30e4ca5d046ca).

