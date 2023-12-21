---
layout: page
title: December'23 -  Reboot
---

The goal of this devlog is to keep myself company as I reboot into development mode. Last few months have been a lot of travelling, hiring, presentations, code reviews and campaigning. Parallelly, I will also be helping the new team get setup. 

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