---
layout: page
title: Week #2
---
Jan 8 - Jan 15 / 2023<br>

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
