---
layout: page
title: December'23 -  Reboot
---

### December 23

Now going further into the workflow, trying to test woodwork design. Woodwork addition and recognition in 3D page are working properly. Modular design page errors out on loading the woodwork. There's an error showing in the console.

This is a chain of issues. The root of the issue seems to be the incomplete patch from yesterday. Woodworks are not loading because the woodwork definition is `null`. Then I checked if the woodwork definition is being sent properly to the backend. It is. Is the definition getting updated in the database. No. I take the bet of converting the definition and supporting attributes of a woodwork also to mutable JSONDicts. Still unable to decide whether that resolution worked or had side effects due to a new error in finding the approapriate bricks for the woodwork composition. 

The bricks needed for creating a woodwork are missing. On digging further it turns out that the bricks are managed via a local cache. These bricks are fetched from the CDN, but stored in the local disk for performance reasons. But, the azure container did not seem to have a copy of these bricks. This did not cause an issue earlier because they were already in the cache. Since, I'm setting the dev environment freshly now, the cache is empty and hence it caused a problem. Fixed it by uploading the bricks from a local backup copy. With that issue resolved, woodworks are loading properly in 3D.

I tested that the woodwork design interface is working alright. Partitioning, sectioning, internals etc. Ofcourse, this needs to be properly implemented in tests later. But for now, I think the deployment is in some shape. 

The next step is to test renders. I did try a couple of preview renders. To monitor, I installed the eccli with `pip install --editable .` The queueing process seems to be working smoothly. I tried running a render worker with the saved alias. 



### December 22

So the furnishing was being added in 2D, but not showing up in 3D. The first thing was checking if all the materials assets were available. Luckily they were. Then on checking the network requests I noticed that the 3D model itself was not being fetched.

- On digging further, I noted that the furnishing was being added to the floorplan, but doesn't show up in the database. I need not have confirmed from the database, but did. So, the frontend seems to be saving a valid floorplan, but the backend is not able to pickup the furnishings in the layout.
- I checked to see if there were any errors logged in the backend. But, none. _As a side note: When I tried to check the backend logs, I noticed a lot drama happening with the worker processes being terminated and recreated a lot. I'll need to resolve that once this is done._
- I tried with a different furnishing. But same story. Successful save. Furnishing saved in floorplan but not shown in 3D. It doesn't show up in the database either.
- Debug log shows the furnishing is "added" in the backend. It doesn't show up in the project in the DB. At this point, I'm actually not sure if it is supposed. But what I can do is check how the scene is being composed on load. The furnishing definitely has to be there.
- Yes, the furnishings are loaded from the Project and the project doesn't seem to be aware of the furnishing even though it is present in the floorplan.
- Figured out what the issue is. The changes are being made to the project but the ORM is not noting the changes. This is very likely a mysql setting. I do remember having to add a config setting to enable the ORM to track changes. This may have been due to a change either with the mysql image or the update to the ORjjjjjjjjjjjjjM dependency. The latter is unlikely because of version freeze in pip. I have verified that the issue gets fixed if the ORM is explicitly notified of the field update. I still need to figure out how to apply this change in the cleanest way possible.


Ok, that's a patch. SQLAlchemy documentation clearly states that the JSON field type cannot track mutations. The recommended workaround is to use the mutable extension that tracks the changes. So, I patched the tables using the builtin JSON type to use the new mutable JSON types. The catch here is that even the extension only supports tracking changes at the first level. Any changes in nested objects of a JSON will not be tracked. This becomes a problem in our case when definitions change. But, it seems when those changes happen we are reassigning the value explicity (I think). So, the main candidates for change are simple lists that track resource IDs.

I'm a bit uncertain about this patch. It solves the problem for now. But a part of the issue may still be present for JSON based dictionaries being stored in the DB. The really strange part here is that this was working fine a while back before my system reset. It should not have been working. If we encounter this kind of issue again, I'll do a thorough pass. For now, I'm committing and moving on.


### December 21

I'm trying to get the dev deployment up. This is the first time that I'm trying to setup the environment myself after the product rewrite. Since I'm doing this with a little more breathing room, I'll try to fix anything that I left over from the original bootstrapping.

The first issue that I'm facing is a permissions issue for the supervisor:
- supervisord fails because it is unable to create its sock file. This throws the container into a restart loop.
- As a first step, I bypassed the default `command` directive in docker compose with a dummy blocker so that I can shell into the container and investigate. I'll leave this in a comment for future benefit.
- When I try to run supervisord from a shell inside the container, it fails in the project's working directory. But, it succeeds in the home directory. So, I guess it is a folder permissions issue.
- The .sock and .pid files are being created whereever supervisor is being run. So, this is likely an issue with having permissions to create the .sock / .pid files.
- I wonder what the default running path for the supervisor is. That would be where the .sock and .pid files were trying to be created. It seems `/var/run/supervisord`. When I manually create that folder, cd into it, supervisor seems to run properly.
- Tried to give the project directory 777 and run the supervisord, it still fails. So, that's strange.
- Ok this is not a folder permissions issue. I tried setting the `user` directive in the supervisor config. The service switches user successfully, but now fails to create the socket anywhere because of permissions and the error code is EACCESS. The issue earlier was EINVAL.
- Oh, I see now. Supervisor fails to create a Unix socket in the container because the default path is the project working directory. That project working directory is actually a bind-mount on docker. So, may be docker's bind mount doesn't support unix sockets being created on the share.
- Ok, one way around this would be to make supervisor run from a different directory, preferrably its default directory.
- Yeah that seems to do the trick. Apparently, installing supervisor already creates `/run/supervisor` and `/run/supervisord` on the container image we're using. Changing the config files to explicitly use that path seems to work.
- I'm still not completely satisfied. It would be nice if this work within the project working directory. May be in the future, we change the container image used and that doesn't have the `/run/supervisor(d)` (may be that image uses `/var/run/supervisor(d)`) folders on installing the supervisor dependency. That would break our build.
- I'm trying to see if there's a way to create a unix socket in the working directory. Internet seems to think creating unix sockets in the bind mount shouldn't be a problem.
- It turns out the purpose of the unix socket for supervisor is just for _supervisorctl_ to connect and doesn't effect the actual functioning of the service.
- Looks like the issue with creating the UDS on the bind mount may be due to the emulation issue on MacOS with the Apple Silicon. Either way, that's not a battle I want to fight especially with the limited importance of the socket in the first place. I've decided to move that to _/tmp/_ which should be good enough pretty much any container image.

Tested. It seems to be working fine. Overall, I'm still a bit iffy about the fix. Updated the prod config as well. Let me come back to this in the future if there's an issue. Added a comment and commited.

The backend is up now. Initialized the db and populated some furnishings. I can now create projects.

Adding rooms is failing. Console shows that the preview images are being fetched from _cdn-test.3dwalk.in_ which is not supporting the http request. This is something new. My guess is that in the last few months, the CDN must have updated its policies that it will not serve over HTTP and mandates HTTPS.

Okay, now we need to fix the requests to use https. Some quick searches in the codebase show that the preview requests are being made on the same domain as the root "//". But the localhost doesn't use https. Hence the cdn requests are also happening using http. Let me explicitly use https for these requests. Yeah, that fixed it.

The rooms are working properly. Fittings also seem to be working. The furniture section shows nothing though. No errors in the console. I'll have to look how those menus are being populated. Looks like all the furnishing opts are available in the frontend but they're being filtered for a repository 'mini-repo'. But, the 'repository' value for the furnishings is 'public'. Updated the filtering criteria and all the furnishings show up in the catalogue. Committed.

The furnishing models still don't show up in 3D. There are no errors showing up in the console either. I'll have to see where the 3D model is being requested from and try to fetch it. I'm guessing this is a catalogue issue. I've to make sure that the catalogues (both materials and the furnishing models) have been properly migrated during the rewrite. I had left that work at about 80-90% last time. That might be what's causing this.

So, first I reset the database. Then I got into my backup and found the .tsv dump for the new materials. That .tsv did not import into the database properly because one of the JSON fields was not properly encoded. So, I wrote a small python script that fixes the broken JSON field in the backup dump. After that, the backup imports into the db without any complaints. That's about 28k materials in the database.

The next step is furnishings. I got the furnishings dump as a .tsv. I was able to import that into the database directly without any issues. With both the tables populated, I now need to first reproduce the missing furniture error. 

With both the catalogue tables in the db freshly imported, I'm able to reproduce the error of missing furnishings in 3D. I added a console log to identify the id of the furnishing that was supposed to show up. Noted down the ID. Checked the slots and noted all the textures that are needed for the model. All of them seem to be available on the CDN. So, that wasn't the issue. Last time I was working on this, I had run a storage account COPY operation on azure that took a few hours to complete and even then a lot of the assets were still in the copy queue. I wanted to make sure this issue was not because of that.

I double checked in a simpler project, just to be sure that all the slot materials actually refer to assets that can be fetched using the ref. On checking the network requests, it seems the 3D model of the furnishing was never fetched in the first place. 


### Intro


The goal of this devlog is to keep myself company as I reboot into development mode. Last few months have been a lot of travelling, hiring, presentations, code reviews and campaigning. Parallelly, I will also be helping the new team get setup. 
