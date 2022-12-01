---
layout: page
title: Migrating azure deployment
---

Due to some administrative constraints, I'm having to migrate our cloud deployment across azure subscriptions.
This is a log of that effort.
<br><br>

## November 2

- Recieved a feasibility and cost estimate of the migration.
- Finished a call with Xencia (MS CSP). Migration seems simple and straight forward, mostly without downtime.
- Shared Global Administrator access to Xencia for both subscriptions.
- Awaiting their confirmation for timings for migration. Likely in the next 2 days.
- The migration has been scheduled for next Friday 6am.

## November 4

Got on the call for the migration at 6am

TODO: Before beginning all the the available resource providers were "registered" for the new subscription. But, those registrations have not been evoked after the migration. This needs to be double checked.

- We first moved the target subscription to the source directory / tenant. Moved the resources to the target subscription and then moved the target subscription back to the target tenant.
- We had a road block moving the studio render workers. Apparently moving spot instances across subscriptions is not currently supported. So, we decided to just move the VHD snapshot to the new subscription and create new worker VMs again.
- Next we moved the app services. We deleted the SSL bindings and the app certificates first. Then created them again after the move. Remembered that studio3d backend doesn't have a custom domain configured.
- We then created a new SSH key in the new subscription as moving SSH keys is not supported.

After the migration, I successfully created a render worker VM with a dynamic ip on the new subscription. But, I realised that there is an issue with the hardcoded azure credentials in the app. Till the app env var config is updated, the app will still try to spin up render workers from the old subscription. Further, the render-worker script itself needs to be updated with new tenent credentials for it to be able to turn itself off.

I have left these changes for a future session as there seem to be some active render work happening on the product and I don't want to disrupt that. I will mostly likely get to it during the first half of the next week.
There is also the task of migrating s3 assets to azure. It also looks like I should document things even for studio3d. I don't think I'll remember all the important things if I come back after a month or two. At this point, I'm not confident that I don't have to come back for a couple of months.


## November 8

- Created spotVMs in the new subscription.
- Created a service principal in azure to let the app spin up the new spotVMs. Got stuck for an hour fixing broken permissions on the newly created SP.
- Realised we have quote for upto 4 worker VMs in each region. But, failed to create workers because location move is not supported for VHD snapshot. Move was not even supported for spot vm instance. This is something I need to check with Xencia.
- Spent another hour trying to figure out why preemptible machines are not being started when a render request comes in. Turned out I forgot to set the appropriate preemptible tag on instances.
- Confirmed that catalogue3d doesn't require any config update due to the migration.

----
<br>


## November 21:

There are a few tasks pending from the azure subscription migration:

- Review and deallocate assets from the old subscription.
- Copy the _render-worker-vhd_ snapshot into a storage account and create duplicate machines in other regions.
- Resolve the permissions issue with SSH into app service in new subscription.

Apart from that, there is another major change. All the cloud assets currently deployed in s3 need to be migrated to Azure Blob Storage. That would save us a big AWS bill. I'm planning to start work on this. These assets are being used by
the production deployment. That adds some complexity.

1. Write an Azure backed _Store_ class in the _emptycup3d_ backend.
2. Create a storage account on Azure for _emptycup3d_.
3. Copy assets from s3 to the newly created storage account.
4. Ensure _emptycup3d_ is working with the Azure backed _Store_ connected to the _emptycup3d_ storage account.
5. Copy all the assets from s3 to the _studio3d_ storage account.
6. Setup a "test" deploy for the _studio3d_ app service and deploy the changes there.
7. Ensure _studio3d:dev_ is working smoothly.
8. Deploy the update to _studio3d:prod_.

- After some consideration, I think it makes more sense to prototype _emptycup3d_ with _studio3d_ storage account.
- Found an implementation for Azure blob storage already in the codebase, but unused.
- Fixed some issues with the existing Azure Blob Store implementation.

Changed the authentication mechanism to use DefaultAzureCredential.
There is also a broken _test_az_store.py_. I revamped it and tried to test the store.
The test failed saying that the request didn't have the permission. But it succeeded in creating the container.
Now for me to assign the right permissions, I need to know which credentials the test is using.
_DefaultAzureCredential_ quietly uses a long chain of fallbacks from environement variables, signed in accounts to browser level sign in. I didn't get any prompt, but my environment is already very complicated with multiple active azure subscriptions, multiple accounts, multiple service principals and mulitple environment configs. So, this _DefaultAzureCredential_ is not a great idea for me. Now switching to an _EnvironmentCredential_.

Made the changes and the auth issue was resolved. Ran the azure store test successfully.

Now trying to copy the s3 assets to studio3d storage account. Luckily, I have already setup _azcopy_ when I was exploring this last time. But, I'm still having some troubles in setting the correct access permissions for the service principal. I had already added _Storage Blob Data Contributor_ and now _Storage Blob Data Owner_. Still the copy command is failing with 403. It was mentioned that role assignments may take upto 5 minutes to reflect on requests. Waiting for that now.

Figured that out now. I missed that _azcopy_ was using AD account credentials. So, I had to add permissions on that account and not the service principal. Did that and now the copy is working with some good numbers ~1300Mb/s.

----
<br>


## November 22:


After more consideration, I decided to avoid the _emptycup3d_ bypass and directly work on _studio3d_.
For two reasons:

1. I may want to implement the _Store_ differently in _emptycup3d_.
2. I avoid unnecessary delay in migration.

With that resolution, I am trying to setup a local deployment for _studio3d_ where I can test the changes.
I had recently deleted the _studio3d_ containers on my local docker to avoid delay's in updates.
Not sure, if that was too drastic and if that was the fix. Having to rebuild the _studio3d_ containers again now.

- Ran into the issue that netlify was expecting node 14.0+ and we were using _node:12-buster-slim_. Updated it now. Building the containers took about 20 minutes.
- Fixed an issue with _artist-app_ build process getting triggered infinitely.
- Fixed an issue with frontend making API requests to production server.
- Fixed an issue with using SSL for dev API.

Facing issues with CORS. Apparently CORS headers are getting set twice. CORS is supposed to get set by the nginx proxy when it receives a request to the backend. I also added _flask-cors_ in the backend itself. That might be causing this issue:
  1. Disable CORS in the backend.
  2. Ensure the request is going through the nginx proxy.
  3. Double check the hostname for the api

Removed nginx from the deployment setup. Website has be to accessed at port 5000 & API is on port 8000. Website connects directly to port 8000 for API request. API has CORS enabled for debug environment. The last change in the API may have to be
merged into master. That fixes the CORS issues.

Next up are some errors with the local db not being up to date with production. Trying to fix that now by deleting the tables in the local db and import the structure of the prod db first and then importing a minimal catalogue. Table delete taking a lot of time. I force quit twice already. I remember having a similar issue last time. In fact, I remember going through this
entire ordeal once before, but I think I was iffy in committing the changes.

After a lot of headache, finally got the DB setup properly. I had force quit SequelAce because it got hung. But, that left an
orphaned mysql process that had a lock on a table. So, when I try to delete that table again or drop the database, it was waiting for the sleeping process to release the lock. To fix this:

1. Opened a shell in the db container: `docker exec -it $(docker ps -q -f EXPOSE=3306) /bin/bash`
2. Logged into the db using the _mysql_ command: `mysql -u root -p`
3. Listed all the processes: `show full processlist`
4. Killed each process: `kill <id>`
5. Dropped the database: `drop database ecdb`
6. Recreated the database: `create database ecdb`

Imported the structure of the prod db. Then imported the mini-repo.

Before I start working on migrating the codebase to use Azure blob storage, I want to commit the working dev environment.
Started updating the submodules. Submodules are just a pain. For every update, I have to update 3 repositories in both _production_ branch as well as _dev_ branch. Yuck!

I realised why I felt like having done all of the dev setup work before. I did all of that earlier in a different branch in the submodule. The submodule branch wasn't on dev and I didn't realise that was the case and made all the changes again in
the _studio3d_ branch. This is really sad. To imagine the team put up with this for so long...I'm amazed at their patience and stupidity.

Testing the dev deployment afresh just once more before moving on...Done.

- Moved the _store_ package changes from _emptycup3d_ to _studio3d_.
- Installed the dependencies manually. Have not updated the _requirements.txt_ yet.

Ran into an error: _ContainerClient has no attribute 'exists'_. I'm using the _exists()_ method to check if the container
already exists. This step was not there in the _store_ implementation earlier. I added it now. The wierd thing is that
Azure's documentation clearly shows that _exists_ is a method on the _ContainerClient_ and the same code worked in the
other repository. This might be an issue with the package version.

----
<br>

## November 23:

I decided to by drop the _exists_ check. It doesn't make sense in the code anyways. I also get to bypass this wierd 'no attribute _exists_' error.

The store seems to be working now. But, the issue is that the db has the resource refs hardcoded. This means for example
that a furnishing record has the s3 url for the thumbnail preview hardcoded in a column. I'm not too inclined to perform
a large database migration on the production db. I'd rather patch the old codebase for _studio3d_ and implement cleanly in the new _emptycup3d_ codebase. Working on the patch now.

Before I started working on the patch. I committed the dev environment setup this time. Further to avoid any confusions, I cleaned up all the branches in the main repo and the submodules. Now, there are only 2 branches:

1. _studio3d_ which is the production branch live on [beta.studio.emptycup.in]()
2. _master_ which is the main development branch. I don't think I want to deploy this publicly. Not sure yet.

Anyways, with a cleaner setup, its time to start working on the _s3-abs_ udpate. Making a list of all the places where
the refs need to be patched:

This feels like wading through a swamp. I added a *patch_ref()* call to _AssetStore_. I used that to update *Layout.to_json()*. But testing any changes is a problem because the API service is not reloading after changes. After a lot of debugging, I realised that an environment variable *ENABLE_GUNICORN_RELOAD* is unset. But, the variable is being set in _docker-dev.yml_. I realised I need to take a break before I lose my gumption.

----
<br>



## November 24:

Fixed that issue. It turns out that there was another place where this environment variable was being reset. Got reload working for Gunicorn. Then ran into another nasty issue with Gunicorn's iNotify system failing on reload. Got tired of this and replaced Gunicorn with the flask development server in the dev environment. That got me back the issue of patching
the store URLs.

Ran into the issue of Flask not reloading on changes. Spent another hour trying to figure out why. Probably because making
changes in the host system doesn't trigger file change events inside the container os. Took a while for me to figure that one out. Anyways, removed flask from supervisord setup and started running it directly from the terminal inside the docker container. If there's an update, I can ctrl+c & rerun the command with the added bonus that the logs are directly visible in the terminal instead of the docker dashboard.

Noticed that the _master_ branch and _studio3d_ branch may be out of sync. That means, I'll have to rebase _master_ on _studio3d_ before merging. I'm afraid that might not be straight forward.

- Got the layout save working after making a small fix in the _store.patch_ref()_ function.
- Fixed CORS issue on the blob service by adding permissions.
- Got Layout 3D working
- Got Furnishings working both in add furnishings & choose colors
- Got Materials working

Only unsure about woodworks now. But that should be working as well. Just need to be double check regarding missing assets.

----
<br>


## November 25:

- Enabled CDN on Azure for the storage account.
- Added CDN functionality to ABS based AssetStore class.
- Added _cdn_ to config.

Incomplete day. Could only clock 2 hours today.

----
<br>


## November 30:

- Fixed issues with CDN functionality within AssetStore & tested locally.
- Updated _master_ in repositories and submodules accordingly. Pushed submodules to remote.
- Cleaned up some stale config / deployment settings.
- Rebased on _studio3d_ branch.
- Created a _master_ slot in Azure App Service for dev deployment.
- Created a github action to publish _master_ as _studio:master_ on Azure container registry.

To publish _master_ also, I need to setup a frontend build as well. I'm starting to wonder whether a separate _dev_ slot is
even needed. Updates to prod will be more stressful for sure. But, I don't expect to make too many updates anyway. Even if I do setup a _dev_ deployment, the diff between _dev_ and _prod_ will again be _non trivial_. So, what's the point?

I have to update the *config_stage.py* first. Then, I'll have to finish rest of the migration tomorrow morning. Recopy all the assets from s3 with --overwrite=ifSourceNewer and then push changes from the local _studio3d_ branch. Restart _studio3d_ app. Test.




## December 1:

- Started running _azcopy_ yesterday afternoon. It has been 16hrs+. It is still running. The --overwrite=ifSourceNewer seems to be a very expensive operation.
- Updated the store bucket names in *config_stage.py*
- Added automatic updation to the render worker scripts.

To push these changes to production:

1. Make clean commits in submodules.
2. Update Studio with the latest submodule references.
3. Push submodules to origin.
4. Push Studio to origin triggering the _studio:prod_ image build through github action.
5. Restart the azure app service.
6. Test the [beta.studio.emptycup.in]() endpoint manually.
7. Preempt render worker shutdown and update codebase.
8. Disable render worker preemption. Shutdown.
9. Test renders.

Issues while testing deployment:

- Woodwork maps have not yet been synced. So, map images are not loading. I started a second _azcopy_ instance specifically for woodwork maps which has been running for a while. There are arround 490k maps which is unbelievable. Warrants some investigation.
- Layout save was failing. On connecting to the container & checking logs, it appeared that AzureIdentity was failing because of environment variables not being set properly. Updated that and published the image again.
- Themes had hardcoded refs to textures. While testing, I didn't run into this issue because I was testing with new projects as the DB was empty. I patched the themes in code to use the updated Azure Edge refs.
- Ran into an ugly patch where texture refs were being patched to get thumbnails for web and HD for renders. Updated that patch to only use Azure Edge refs.
- Updated all hardcoded _ecdn.in_ refs in the frontend codebase.
- Ran into the issue of a lot of .ktx thumbnail resources 404ing. Tried to dig into the root cause. Found that these resources were not present even in the source buckets. Not sure why that is. Left it be for now.
- A bug in patching woodwork side refs was blocking 3D model load. Fixed it and am now able to see the 3D model load properly in production.
- Render previews are loading properly as well.

The s3 to ABS transfer is still happening though.
