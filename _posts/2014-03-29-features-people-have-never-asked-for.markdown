---
layout: post
title: "Meld features that people have never asked for"
date: 2014-03-29 09:45
comments: true
categories: [Meld]
---

People ask for new features all the time. Sometimes they're good ideas, sometimes... they're not. Sometimes there's a better way to address the requested feature. However, to me it's interesting to contemplate the things that people *don't* ask for.


New Window
----------

Meld is a single window app. It isn't designed that way... it's just that it's never supported anything else. No one has *ever* asked to be able to open a second window.

In Meld 3.11.0, we now at least have the notion of windows, though we still don't actually have a 'New Window' menu item. Maybe one day...


D-Bus API
---------

Meld uses D-Bus to support some very limited single-instance features; specifically, you can open a comparison in a new tab. However, no one has ever expressed any interest in having an actual D-Bus API for Meld.


Move to Trash
-------------

We do some really terrifying things when handling folders and directories, the most obvious being that you can recursively and permanently delete folders from within a folder comparison. Permanently deleting files doesn't even prompt! Despite this being a pretty nasty example of not handling user error, no one has ever suggested that maybe we should be less insane.

In Meld 3.11.0, we use GIO to 'trash' things for us, which should do-the-right-thing on different platforms.

