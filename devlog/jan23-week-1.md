---
layout: page
title: January 2023 - Week #1
---


### Monday

At close of work last week, I was trying to get the UI controls to position intelligently.
When the top right section of a box is to thin, the UI controls overlap on each other breaking accessibility.
I tried implementing a _isCluttered() method and using that to position component controls. That didn't work out as planned
and ran into a few unexpected corner cases where it breaks.

I'm now planning to try an alternate approach. Everytime a control is set, I'll adjust the position of
all the enabled controls appropriately based on their bounds which should be more reliable.