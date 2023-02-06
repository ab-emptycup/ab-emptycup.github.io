---
layout: page
title: Jan Week 5
---

Jan 29 - Feb 4<br>
Week#: 5/52<br>
<br>

### Hour 39-42:

Wrote and sent the investor update after almost 9 months.

----
<br>

### Hour 37, 38:

Worked on issues for EmptyCup Portfolio. Had a call.

### Hour 35, 36:

Started trying to implement the patch I worked out yesterday. That turned out to be too complicated.
I don't have the mental model of how the layoutplanner library works in my head. I figured it might be too
time taking to figure that out now, given the poor naming conventions and lack of comments. Gave up on that patch.

The alternate would be to scale the walls of balcony appropriately (floor_width - wall thickness). But, that might
also be complicated due to the way scaling is implemented. _WallCornerConstrainer_ seems to be responsible for this.
I'll take a shot at hacking that.

I'll soon have to take time out to wrap my head around the LayoutPlannerJS library.

### Hour 34:

Completed & logged a book I just finished: [Rework](/books/rework) by Jason Fried of 37 signals.
Talks about startups, product development, marketing, culture, productivity with basecamp as a case study.

----
<br>


### Hour 33:

Floorplan optimisation is a dense piece of code. Been studying to identify all the possible cases.
I have worked out a simple patch in pseudocode to fix the issue and give the extra power of handling variable height walls.
I haven't started implementing the patch though.

### Hour 31, 32:

- Started working on fixing balcony scaling.
- Walls now extend the entire depth of the balcony.
- Walls now scale with the balcony floor.
- Found an issue with composition when a balcony wall joins a full height interior wall.
- Digging into the floorplan optimising code to fix the issue.


### Hour 30:

- Fixed the issue of individual walls of a room not scaling properly. Just enabled scale controls on selection.
- Noted an unintended side effect of the scaled wall sometimes losing free movement. Workable for now.

### Hour 29:

- Merged the _nossr_ changes into _master_.
- Started working on LayoutPlanner fixes in _layoutplanner_ branch.
- Reorganised the flat svelte component files into UI module folders
- Tested and fixed all issues successfully.


------
<br>

### Hour 23-28:

! Bad logging practice detected !

- Removed all dynamic imports from the frontend svelte codebase.
- Fixed the issue with layout id and project id being _undefined_ on first project page load.

--------
<br>


### Hour 22:

Had a quick UX test with my wife. A couple of useful insights:

- Furniture mode is needed. Room gets selected and moved unintentionally too often.
- First person navigation is a great challenge. Need a simpler navigation model. Scroll is too sensitive.
- Hanging items will also be looked for under ceilings.


### Hour 20, 21:

- Designed the floorplan all over again.
- Identified a few issues:
    - Components getting rotated automatically.
    - Balcony walls breaking up exterior bathroom walls improperly.
    - Scaling rooms don't snap
    - Walls part of a room cannot scale.
    - Rooms not getting copied properly.
    - It's hard to differentiate surface depths without lightmaps.

### Hour 19:

- Started debugging the layout save issue that dropped the entire 2 hour work today morning.
- I'd forgotten to update the production db after the last Layout model fix.
- While trying to connect to _ecdb_, realised that this was probably the 10th time I have had to add dev machine ip to ecdb firewall manually.
- Crafted a bash function in _dev.sh.rc_ to automate this. Tested successfully.
- Updated the production table successfully.


### Hour 18:

- Closed yesterday's thread to backup s3 assets as is into ABS.
- One of the transfers failed. Had to jump through some hoops to figure out which container failed.
- The last container seems to have failed due to some bad permissions on the source bucket.
- Note: Had a call with Rishab regarding GPU renders on Azure cloud.


### Hour 17:

 - Realised that our LayoutPlanner is good at drafting a given floorplan, but a pain at planning the original floorplan.
 - The real bummer though was that the entire work got lost after the layout save failed due to some 500.

### Hour 15, 16:

 - Cleaned up, rebased and pushed the latest code to production.
 - Started designing a house on production.
 - Noted a bunch of issues.


-----------------
<br>

### Hour 14:

Considered the possibility of reordering the s3 bucket copy. But, that didn't seem like a robust solution.
Noticed a couple of cases where that approach would fail.

Decided that the best thing to do now is let the old catalogue be. But the S3 account will be closed soon. So, I decided to make a copy of the entire storage into a separate Azure storage account. Created a separate "archive" account for this on Azure and assigned the necessary roles.

Crafted the scripts to perform the copy of 31 buckets in total from 3 parallel processes. That's around 1.5TB of data that needs to be moved. The copy will take some time. Even at a cumulated average of 100Mbps (which might get throttled down), the copy op will take a few hours.


### Hour 12, 13:

- Made a few changes to the patch. But ultimately decided to drop it.
- Ran into a new issue when exploring the old catalogues. Some of the topviews are broken. Though the asset references in the db seem to be correct.
- This is a consequence of a few bad decisions taken in the early days. Keeping _ref_s in the db is the major one. Turns out over the times, we added refs from multiple different buckets and CDN endpoints into the db. During the recent S3 to Azure migration, the buckets were copied into a single container causing overlaps between _devel_ and _prod_ buckets randomly.


### Hour 11:

- Found the issue. The default material has been replaced during the recent component material normalization.
- Tried a patch to use the original material. Seems to be working.
- But it seems this is not a bug. Just a bad selection of default materials.
- On digging further, it seems the normalisation of materials was not a very popular move:
    - Users can't differentiate the models now.
    - Everything looks similar.

I'll have to rethink the whole auto texturing idea. But, no point doing that with the old catalogues.
I'll keep this in mind for when I start working on the new catalogues.


### Hour 10:

- Fixed the issue with the build. JS compilation was triggering build by modifying the .js files in _libs/xxx/build_
- Started debugging the missing default material. It seems a different default material is loading. Likely from the default palette.


### Hour 9:

- Turned out that the libs were not being recompiled in the build step.
- Added build step, but now the frontend breaks.
- On debugging, it appears _nodemon_ is stuck in a reload loop.
- My best guess is that the jslib build is triggering _nodemon_ which invokes build again.

### Hour 8:

- Got a fresh copy of the catalogues from the production db and imported.
- Reproducing the issue of missing default materials on the dev machine. Success.
- Not able to debug using _console.log()_ due to frontend not refreshing on code update.


### Hour 7:

Getting back to the dev setup issue. I need to address this before I can debug and fix the issue with missing defaults materials for components.

- Restarted the system.
- Disabled restart for _artist_ containers.
- Rebuilding the _artist_ containers.
- Got the deployment issue fixed. Forgot that the dev api needs to be run manually now.
- Erroring out becasue the local DB is out of sync.


### Hour 6:

Wrote up my thought process for getting the user onboarding experience right. Looking to find someone with direct experience who can guide me on this.


### Hour 5:

Investor sync up call

### Hour 4:

Started debugging the issue with missing defaults for components in Studio 3D. Ran into issue with getting the dev environment to run.
Gave up unable to figure out the root cause. The API endpoint seems to be returning empty responses. API requests are not showing up in the logs.
The dev setup has become a huge pain with too many moving parts.

### Hour 3:

- Blocked for an investor call. Got rescheduled.
- Setup a product review call for coming wednesday.
- Started the monthly review of finances.

### Hour 2: Weekly setup

- Set productivity goals
- Identified tasks to work on. Updated tracker:
    - Fix missing default materials for Studio3D (12 hours)
    - Fix modular UI scroll (4 hours)
    - Fix layout first load (4 hours)
    - Revamp the _svelte_ import pattern (4 hours)
    - Buffer to fix bugs (12 hours)

- Identified creatives to work on.
    - Portfolio v0.1 issues
    - New product demo video

- Schedule calls:
    - Product onboarding call
    - UI/UX review call
    - Investor update call


### Hour 1: Last week review

- Reviewed GTD. Missing daily visits. That's why the routine is lacking oompf. But then the tasks are also low priority.
- Missing daily task tracker reviews. This needs to be addressed this week.
- Finished [devlog summary](/devlog/jan23-week-4)


-----
<br>

Stretching the week a bit this time:

- 36 hours of dev work
- +4 hours of calls
- +10 hours on planning & creatives
- 50 hours of work in total

This is probably the maximum hours I can spare for work in a balanced schedule.

With regards to logging:

- I want to log non dev work also (devlog -> worklog)
- Maximum log chunk can't be for more than 2 hours. Preferrably, always 1.

Pitfalls to be mindful about:

- Don't leak hours during the first half. Especially @ 10-11am.
- Plan the afternoon's creative work a day in advance in the background.
- Pace myself. Don't get winded.
- Be prepared for a mid week motivation slump. Noticed this last week. Stop thinking. Just keep going.