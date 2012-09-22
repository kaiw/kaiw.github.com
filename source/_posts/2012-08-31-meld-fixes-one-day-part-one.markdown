---
layout: post
title: "Meld fixes I'll never get around to, August 2012 edition"
date: 2012-08-31
comments: true
categories: [Meld]
---

Our automatic merging commands 'Merge from left', 'Merge from right' and
'Merge all' depend on the focussed pane. There are two problems with this.

Firstly, for most people, merging goes from the outsides to the middle, and
never in reverse. The reason is that this is how it works for version control;
merging in VC always (not actually, but close enough) involves making changes
to *one* file with reference to the other two. As such, it would be reasonable
to expect that 'Merge from left' actually merged all of the left pane changes
into the middle pane, regardless of where the cursor was.

The second problem is that 'Merge all' makes *absolutely no sense* in any pane
other than the middle; it's identical to 'Merge from right' in the left pane,
or 'Merge from left' in the right pane, but more confusing.

One option would be to rework these commands so that they only ever operated
on the middle pane. Another option would be to add some dynamic labelling so
that it was clear what the menu item did before you clicked it. Without
knowing how widely used these actions are, and what people use them for, it's
hard to know what the best option is.
