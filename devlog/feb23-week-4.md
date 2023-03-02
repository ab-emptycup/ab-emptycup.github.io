---
layout: page
title: February Week 4
---

Feb 26 - Mar 4<br>
Week #: 9/52<br>

### Wednesday: Mar 1

Retrospective logging again:

- Changed some of the DB columns to JSON type before importing furnishings.
- Surprisingly the original TEXT columns converted to JSON type pretty smoothly.
- Fixed a bunch of initialization issues with the codebase.


- Dropped the _tag_ tables.
- Dropped the *project_access* table.


- Removed a lot `looks` code. Dropped the notion of multi-theme projects.
- Removed `active_theme`. Tested successfully with some quirks.
- First, there still are some materials hardcoded in code that refer to _studio3d_ assets.
- Second, _slots.json_ used by `house.create()` still references _v1_ material ids.


- Streamlined the furnishing recataloguing flow.
- Standardized the file naming convention for the recatalogue pipeline.
- Cleared up the _emptycup3d_ blob containers.
- Setup script to import the ~15000 furnishings after recat preprocessing.
- Running copy. ETA 6 hours.



----
<br>


### Tuesday: Feb 28

**27950** materials linked as defaults for the components in the _artist-v1_ catalogue are from an older catalogue.
**22016** of these are categorized as of type _misc_. I need to figure out a way to categorise these intelligently
to move them to the new repository. One consideration is to use the slot selector of the component to tag the material.
But, that may not be accurate. A few issues:

1. There might not be a _type_ based selector to infer the _type_ for the default.
2. There might be multiple _type_ based selectors. How to pick among them?
3. The default material might not actually be of the _types_ listed as selectors.


Well, I guess the way forward is to take what we get. It is atleast better than _misc_. So, the next steps are:

1. ~~Filter all the default materials into a separate file.~~
2. ~~Generate a mapping based on the above "hack".~~
3. ~~Transform the category meta data for the filtered materials.~~
4. ~~Reslot the materials.~~
5. Merge the materials with the existing filtered materials.
6. Recheck default materials for the filtered furnishings.

Looks like there's about 75% recouping of data. The accuracy / relevance in that 75% is still a question.
I don't want to be too thorough now. I probably should be. But, meh. I'll skip the last 2 steps.

Next, I want to check the preview images for all the shortlisted furnishings to see:

- If there are any obviously bad furnishings...
- If the default materials are looking decent...

Turns out that a lot of the materials are fine. But there is a significant portiona that is not good.
Here's a list of issues that I found out:

1. Some of the components (sofas, I think) have random materials making the component look clownlike.
2. Some of the components have bad defaults (again sofas) that make them look brownish and dull.
3. Some of the components are bleached.
4. Some of the components are completely transparent.
5. Some of the components appear decimated.
6. The components with lights don't have emissivity set for bulbs.
7. The components with metals don't have specularity set.


I tried filtering the components with bad materials manually and it seemed too much of an effort.
I don't have the energy to climb mountains now. I want to keep the efforts small and incremental.
So, I figured the next steps for me:

1. Import the filtered catalogue into a new db
2. Implement scripts to regenerate preview images and update
    - Check if the component has been used in projects before
    - If yes, extract the component materials from the project's theme
        - Import the component materials into the new database
        - Regenerate the preview image
        - Update the component slot defaults
    - If no, randomly select one of the prebuilt palettes.
        - Import the applicable materials into the new database
        - Regenerate the preview image
        - Update the component slot defaults
3. Clean up the bad furnishings incrementally in batches.

I want to finish this optimistically in 2 days. That should wrap the catalogues work for now.
Then the plan is to:

1. Update the production db
2. Test a project creation flow on [emptycup3d.com]()
    - Documenting test flows
    - Woodwork creation
    - Testing renders
    - Adding furnishings

PS: I also need to fix the custom door issue on [beta.studio.emptycup.in]().

+ Setup the material import script. **28k** materials to be imported. ETA 4.5 hours.


----
<br>

- Continuing work on catalogues.
- Feels like I need to get more productive even by jungle standards.
- Improvise and improve logging.