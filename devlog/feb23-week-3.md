---
layout: page
title: February Week 3
---

Feb 19 - Feb 25<br>
Week #: 8/52<br>


### Thu, Feb 23

Removed _Furniture_, _Looks_, _Palettes_, _Exports_, _Design Themes_. Tested successfully and commited.
Added a note in commit message to fork here if the code is ever needed again. I was delighted to find
that the code didn't have too tight an integration with the core system.

Now that the lot of unnecessary code is gone, I'll work on scripting the catalogue reports. I don't want to
touch the _slots_ just yet. First up is materials.

Implemented `ec tools recat analyse`. Decided to under engineer the tooling compared to last time _s2e_.
Got a report of all the materials with repositories, categories and subcategories. _artist-v1_ looks promising.
But even that needs some clean up. Still, its a very good starting point.

Just taking a step back to evaluate what catalogue functionality needs to be supported now. I'm wondering how much
power is needed in the system to enable onboarding brands. That would enable integrations and that's power. I have
to weigh that off against the practical approach of focusing on what matters today. I made a map of the catalogueing
functionality that I can think off.

Implemented `ec tools recat filter` to filter materials. Used that to filter materials from 'artist-v1' repository.

Implemented `ec tools recat map` to generated a map of types, categories and subcategories.

Manually went through the map of around 400 material categories to clean up their categorization and conventions.
May have to make a few passes through the map to reach reasonable cleanliness and sanity.


----
<br>

### Wed, Feb 22

I pushed the v0.2 version to production already. There are some painful issues still:
- Ceiling previews are now black
- Untested completely

But, I feel like working on catalogues now. I just want to get that big thing out of the way first and then focus on the
small things. Catalogues is no joke and it is blocking because new users can't signup because of it even if they're willing
to put up with the bugs.

Here's what I have on my plate:

- First I need an analysis of all the exisiting furnishings.
- I also need a top down break up of the furnishing categories.
- I need to clean up the palettes, slots, furnitures code.
- I need to add the 'upload' flow for new components.
- I need to merge the UI for selecting furnishings in LayoutPlanner and ModularUI.
- I need to add facility to customise door models
- I need to add facility to customise handle models
- I need to organise materials
- Redo previews for all the furnishings and components.


-----
<br>

Starting this week's log on a Thursday. Need to reflect on how to log when not coding.
