---
layout: page
title: Jan Week 4
---

Jan 22 - Jan 29<br>
Week#: 4/52<br>

### Hour 27, 28, 29, 30:

EmptyCup 3D:
    - Fixed an issue with lightmaps being loaded from old S3 stores.
    - On digging further, found that fallback material was getting set.
    - Textures are not being passed to the frontend after the *raw_query()* to get all materials.
    - Patched the *raw_query()* function to add texture ref attributes whenever appropriate.
    - Further textures are not being loaded due to the saved theme flattening the texture less materials. Worked around that.
    - Now texture are loading properly.
    - Noticed two issues where:
        1. _.ktx_ versions are being requested for textures that are not available.
        2. Some furnishings are not loading in 3D, probably due to errors in loading materials due to 1.

    On further investigation, found that the furnishings are loading, but really late. May be an issue with cache / not having CDN on dev. Not sure really.


### Hour 26:

- Started debugging materials issues. Studio 3D and EmptyCup 3D.
- Studio3D:
    - Tested a couple of components shared in the bug report. This may be issue with new component uploads.
    - The default material is showing up as white for a lot of components, not just newly uploaded.
    - If there's some issue with fetching the material in the UI, the default white material is used.
    - Gotta start with Walkin Loader to see why the fallback material is being applied.
- EmptyCup3D:
    - Materials seem to have textures and the texture images are accessible on the CDN.

I was hoping these were related issues. But, apparently. It's a bit disorientating to pursue both threads at the same time. I'll focus on fixing the Studio3D issue first. They have been due for over 2 weeks now.


### Hour 24, 25:

- Added _AssetStore.delete_asset()_
- Updated Layout model to md5 hash of definition as refkey.
- Updated the column in table.
- _Layout.update()_ now computes the new hash, saves new model composition and deletes old assets.
- Tested on local machine successfully.
- Evaluated hashing and testing on client. Dropped the idea to keep things simple.

------
<br>

### Hour 23:

- Fixed issue with error highlighting failing on Layout canvas.
- Started debugging issue with layout save inconsistency
    - Dev setup seems to be running fine.
    - Production is running into issues of assets not updating.
    - My best guess is that the CDN is not updating on asset save.
    - One option is to create house models based on the layout hash and delete the old model.



### Hour 21-22:

- Created blog on [emptycuphq.medium.com]() after some consideration for alternatives.
- Linked both the [blog](https://emptycuphq.medium.com) and [tutorials](https://emptycup.gitbook.io) from product.
- Fixed issue with Switch component not changing state.

----

### Hour 12-20:

- That was a mad effort to get the render farm working properly. Recreated the render worker half a dozen times to get things working smoothly.
- Dropped the entire cache disk notion after over pouring 10-12 hours into it. That was very poor foresight. That choice added a tonne of complexity to the render worker's setup and startup while saving a few hundred bucks. I decided it wasn't worth it at the end and dropped it.
- Fixed a bunch of other issues with the setup and startup scripts including issues with 'cache' and 'data' dir paths.
- Suddenly the blender mirror went down breaking the entire setup script.
- Changed azure vm shutdown mechanism from the old hardcoded API based method to using Azure CLI which is much cleaner.
- Also revamped the latch to stop auto shutdown by adding a 'burst' tag to the VM on the Azure portal.
- Tested renders successfully now.

8 hour effort turned into 20 hours again :'(


### Hour 11:

- Started testing *render_worker_startup.sh*.
- Fixed broken path to _tmp/cache_. Removed some seemingly irrelavent code.
- Fixed a couple of issues with missing environment variables.
- Decided to streamline the mechanism for setting environment variables.


-----
<br>


### Hour 9, 10:

- Setup the render worker again.
- The cache disk is not auto mounted on boot. Adding the entry to fstab is still manual.
- Fixed the script to confirm partitioning.
- Fixed the script to add entry to fstab after confirmation.


### Hour 8:

- Fixed the issue in the script by asking the user to input the right device id.
- Reran the script by mistake which wipes the unclean _emptycup_ folder. Unfortunately the root filesystem was mounted as cache. Since that was a duplicate mountpoint it didn't show up in _lsblk_. This ran rm -rf on the root filesystem which was mounted as _cache_ fucking up the VM.
- Now setting up the render worker again.

### Hour 7:

- Renamed the render workers & queues to have prefix _emptycup3d_ instead of _ec3d_ to avoid inconsistency.
- Created a new VM with the new prefix _emptycup3d-_
- Moved the setup script and keys to the newly created worker.
- Ran the setup script to setup the render worker. Failed silently.
- Script failed. The cache disk was getting added in a different device order.

### Hour 6:

- Checked if the Azure cloud credentials are correct.
- Checked if the new code is able to find VMs in the _studio3d_ deployment. It did.
- Figured this must be a permissions issue.
- Fixed by giving the service principal permissions to the render workers resouce group.
- Tested the job is successfully getting queued.



----
<br>

### Hour 5:

- Setup and mounted the cache disk.
- Changed the cache mount point from 'tmp/cache' to 'cache'.
- Renders still failing in the manager queue becase *cloud.get_nodes()* is not showing any VMs.


### Hour 3, 4:

- Fixed a bunch of issues with the setup script.
- Added devops key to the render worker.
- Tested unsuccessfully. Rendering failed because 'tmp/cache' doesn't exist.

### Hour 2:

- Created `ec3d-standard-render-worker-0` in a separate resource group.
- Added a 64GB Standard SSD cache disk to the VM.
- Implemented a setup script for setting the worker VM.


### Hour 1:

Getting started with setting up renders:

- Fixed the issue with _cloud.run_node_ and deployed to _production_.
- Tested rendering. Job queued in worker queue. Manager failing due to _NotImplementedError_. That error was getting triggered
due to lack of suitable render nodes in the cloud.
- Started adding a render worker


---

Last week was good in terms of consistency, ok in terms of productivity, unfortunate in terms of output. I'm want to just
keep it up this week. There might be an off day on 26th. Accounting for that I'm aiming for 30 hours this week.

A few pointers from last week:

- May be I need to be more precise about time when logging work. But, not sure, if it is even so important.
- I should definitely use the timer more often and more effectively.

The tasks that I want to wrap up this week:

- __4 hours:__ Setting up rendering on [emptycup3d.com]()
- __4 hours:__ Fixing page scroll issue in ModularUI.
- __2 hours:__ Fixing small component move in ModularUI.
- __4 hours:__ Enable partition deletion.
- __12 hours:__ Fix textured materials.
- __28 hours:__ Fix studio3d issues:
    - __8 hours:__ Missing default materials for components.
    - __8 hours:__ Improper UV scale for walls in 360 renders.
    - __12 hours:__ Line shadow at 7' height


Planned for 54 hours. Available time is 30 hours. Fingers crossed.