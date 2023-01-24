---
layout: page
title: Jan Week 4
---

Jan 22 - Jan 29<br>
Week#: 4/52<br>


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