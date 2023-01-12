---
layout: page
title: Jan Week 2
---

Jan 8 - Jan 15<br>
Week#: 2/52<br>

Most of last week was spent in planning. Essential overhead. This week I want to focus on publishing.

### Sunday:

First question is, do I keep a separate deployment for beta / edge?

The only think I"m concerned about is: I'm not sure if I want to keep project ids, asset ids. For beta, I want to keep
the old database. But, I want to reset the database once before going into stable. From then on, I'll guarentee backwards compatibility.

I've decided that I'll deploy directly on [emptycup3d.com](). Once the version is stable, I'll fork the Edge deploy. Main criterion for this decision was to reduce as much complexity upfront as possible.

There are a few things to do before [emptycup3d.com]() is live. First I want everything to work smoothly on my local machine.
Last time I tried to design my own house. I got stuck at furnishings. I'll pick that back up and setup the furnishings DB.

1. Fix the store implementation.
2. Create storage account on Azure for _emptycup3d_.
3. Filter good furnishings from current produciton db.
4. Script migrating a furnishing between versions.
5. Migrate filtered old furnishings to new version.
6. Save a copy of local db dump.

Before starting that, I fixed a couple of open issues on ModularJS. Then, I rebased all the work on ModularJS and
 merged with master. There're still quirks, but the rewrite is now in a near complete stage.

- Updated the new ABS based AssetStore.
- Fixed store config
- Cleaned up environment config: EMPTYCUP_ENVIRONMENT = (development, production)
- Created _emptycup3d_ storage account on Azure
- Fixed issues with _eccli_ after the config update


### Monday:

Reviewing week's sprint: <br>
Total hours planned: *44*<br>
Total days available: *5*<br>

Todo:

- Setup furnishings database
- Setup materials database
- Deploy on [emptycup3d.com]()
- Setup render workers
- Refresh woodworks in 3D after save
- Fix broken scroll for ModularDesignModal
- Enable deleting partitions
- Fix move control for ledges

Today:

* Patched Furnishing table to drop ref columns in favour of a _refkey_.
* Ported `ec db reinit` and reinitialized the dev db.
* Patched Material table to drop *texture_ref* column in favour of a _Material.refkey_.
* Patched Layout table to drop _*\_ref_ columns in favor of a _Layout.refkey_.
* Patched Woodwork table to drop _Woodwork.refs_ column in favor of _Woodwork.refkeys_.

That was about 4 hours of work today excluding planning. Way below my expectation.
Productivity was B class. Can do better.


### Tuesday:

Testing the _refkey_ changes. Fixed a whole bunch of issues to get things working after the changes.

Setup `ec tools s2e furns` to import furnishings from _studio3d_ to _emptycup3d_.
This looks like it is going to be more complicated than I thought.
Is this a one time thing or do I need to keep doing this. If latter, I need to figure out a way to connect to both the old database and the new database.

Today was a long day with 7.5 hours of productive work.

### Wednesday:

- Export old furnishings database as tsv.
- `ec tools s2e furns` now takes a `--sourcep` optional input to load the tsv file.
- Implemented furnishing import and tested.
- Implemented furnishing asset copy on import and tested.
- Filtered all _mini-repo_ components.
- Migrated all the filtered components (count: 2331) to new db.

UI still seems to be broken. Haven't dug into what the issue is yet.
I could only manage 4 hours of productive work today.


### Thursday:

Fixed the issue with broken furnishing previews in the UI.

Having issues with _theme_ because none of the materials referred to in the theme are available in the db.
The challenge here is that even if I import materials from the old db. They wouldn't have the same IDs.
But then that is the case with furnishings as well. So, none of the old projects would work on the new deployment.
Then reason for material error must be that the materials used in the base house model are also not present in the db.

So, I have to first import the base materials. Then replace the references to these base materials everywhere in the code with IDs of the newly imported materials. Doesn't feel like fun :'(

1. Search where the default theme / materials are being set.
2. List all the default materials.
3. Implement script to import materials from studio3d to emptycup3d.
4. Import all the default materials into emptycup3d.
5. Test that the 'theme' functionality is properly working.

- Done dumping furnishings
- Done loading the old db into `ec tools s2e mats`
- Implemented importing material
- Implemented texture copy

Long day about 7 hours of work. Quality of time is not too good.
Having troubles maintaining stable energy levels through out the day.

### Friday

- Fixed a few issues with ref copy
- Struggled a bit with filtering materials.
- Could not decide how to deal with base materials. Partilly implemented an importer.
- Decided to import the whole materials database.
- Fixed issue with _hash_ column being UNIQUE in the Material table.
- Dropped 2 hours of import progress after realising thumbnails were not being copied properly.
- Restarted import process after fixing issues with log update. Been running for 3 hours by EoD.

Today was about 3 hours of work. Not able to keep up with the intensity and consistency needed for this.
I need to work on myself to be efficient at this.


