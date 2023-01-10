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


### Monday

Testing the _refkey_ changes. Fixed a whole bunch of issues to get things working after the changes.

Setup `ec tools s2e furns` to import furnishings from _studio3d_ to _emptycup3d_.
This looks like it is going to be more complicated than I thought.
Is this a one time thing or do I need to keep doing this. If latter, I need to figure out a way to connect to both the old database and the new database.


