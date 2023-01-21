---
layout: page
title: Jan Week 3
---

Jan 15 - Jan 22<br>
Week#: 3/52<br>

This was a good week. Starting to see some semblance of productivity. Not setting too high of an expectation in terms of hours was a good call. It let me push through the week without getting anxious. 36 hours of coding seems to be my sweet spot.

Hourly logging was a good idea. It let me manage pace without too many jerks.

The gross misjudgement of effort needed to deploy was unfortunate. But it couldn't be helped. I'd rather have worked than spent a day planning. I'll try to be more conservative about task estimation though.



### Hour 38:

- Deployed [emptycup3d.com]() successfully.
- Tested project creation, layout save, adding furnishing, tried render preview.
- Preview not rendered. `ec renders monitor` shows successful addition to worker queue.
- Manager Job failed due to issue with _cloud.run_node()_


### Hour 37:

- Made 'EMPTYCUP_RENDERS_QUEUE_PREFIX' an environment varible. Everyone else derives from it.
- Added task to setup all environment config variables in one place.
- Tested changes locally. Cleaned up repo and committed to _renders_ branch and pushed to production.


### Hour 36:

- Successfully cleared render worker queues with `ec renders process`. Validated 2 preview renders in dev deploy.
- Implemented `ec renders show <rid>` to get the details of a render from Render.id
- Inconsistency in Render.status when manager errors out after enqueuing a job in a worker queue. Added task.


### Hour 35:

- Jobs were showing as missing in queue because the queue name was not right. Fixed it.
- Jobs are now getting stuck in the Manager queue. Again, because manager was looking in the wrong queue. Fixed it.
- Jobs are now failing in the manager queue because manager is erroring out when trying to spin up a cloud worker.
- Fixed the issue by resetting the environment variables for _config.renders.cloud_prefix_.


### Hour 34:

- Implemented --drop for `ec renders santise` to drop orphaned records.
- Cleaned up old records. The latest 2 records exist, that are neither orphaned nor in queue.


### Hour 33:

- Tested the local render request flow. Need to test the render job processing flow.
- I need to setup _eccli_ from dev host to be able to use `ec renders` outside container.
- Fixed environment issues to run `ec renders` outside container.
- Render Job is being created in the DB, but queues are empty.
- Fixing issues with `ec renders sanitise` first to start debugging the original issue.


----
<br>


### Hour 32:

- Renderer seems to be recieving a stripped down furnishing object which doesn't have the needed attributes.
- Side note: Frontend can be cleaned up after disabling SSR. Added task.
- Renderer is expecting the furnishing data in the render request. But frontend doesn't send it.
- Side note: Need to create a separate route for 3D. Added task.
- Fixed by adding the data in the initial response sent by the backend.
- Better fix is to let Renderer figure out the right refs using the refkey. Added task.



### Hour 31:

Next up: Setting up rendering.

- First things first, cleaned up all the local and remote branches except _master_ & _production_.
- Tested local rendering functionality. Material application seems to be broken. Fixing that first.
- Done. Material application now working as expected, but textures are not loading. I'll come back to it.
- Requesting a day light preview render gives a 500. Debugging now.



### Hour 30:

Fixed. Issue was being caused due to not checking if house model asset exists when getting ref. Fixed now.

Development and production are writing to the same storage account, which is a bit troublesome. But otherwise, production is ready. I'd consider the deployment task complete.

A few todo items come to mind:

- Comment code as much as poossible inline. Especially describing what's being done.
- Separate AssetStore for production and development.
- Move eccli.egg-info to eccli's build directory

### Hour 29:

- Fixed a bug in *AssetStore.get_cdn_url*
- Loading furnishings successfully in 2D on production.
- Layout save failing with 500.
- Reproduced issue in development.


### Hour 28:

- Cleaned up build config & pushed.
- Build succeeded on netlify.
- Deploy succeeded on [emptycup3d.com]().
- Imported latest furnishings & materials to ecdb.v2



### Hour 27:

First I want to confirm that this is the popperjs issue and not a consequence of bad build config on my part mainly because the error with popperjs was different if I remember right. There's a temporary patch that should work if this is really the popperjs issue. Trying that now.

Applied the patch. Worked locally.

----
<br>

### Hour 26:

That was a huge mind fuck. Build was succeeding but the deploy was not working. So, I setup _vite preview_ to preview the build locally and started running into a different _500 internal server error_ issue that was being caused by _@popperjs/core_. After digging through the popperjs discussions on sveltestrap, even the temporary patches suggested there did not work. I guess, I'll have to take a break and come back to this issue. This popperjs issue has been irking since the very beginning of sveltestrap and the project isn't being maintained. So, the situation isn't ideal.


### Hour 25:

Decided to roll back commits till this issue is resovled. After 3 iterative deploys, figured the issue was the "build" directory change. I'd made a few polishes along with that change that masked the issue. Updated the build config to get the build to succeed again.

But ran into a new issue now. On navigating to the deploy, a message "The page you are looking for doesn't exist." shows up.
On checking the build folder, I figured that the build only contains one html file: `200.html` which was added as a "fallback" option.


### Hour 24:

I'm not sure what the issue is. Prerendering should be off. I have explicitly set it to _false_ at two points and the default value itself is _false_. Still the error sayes prerendering failed. May be something else is the issue and this error message is bad reporting.

The error is occuring inside svelte-kit itself. `Unexpected token 'export'`. Having some trouble figuring out the root cause.

### Hour 23:

- Found an option for disabling prerendering completely and operating in SPA mode. That seemed more relavent to what I'm trying to do. So, configured that. Local build succeeded and the app is loading fine.
- Deployed to Netlify. Build failed with error 'build' directory does not exist. _sveltekit_ seems to be building to _.svelte-kit_ folder and netlify was configured to look for the build in _../../build_ relative to webapp src. Fixed that.
- Ran into some other issue where suddenly prerendering got triggered again. Not sure what caused it. Still debugging.


### Hour 22:

- Been digging around to understand what is going on. There's a detailed issue on Github on a similar issue. But, not too sure if that's my fix. But I need to understand prerendering a bit more clearly, especially prerendering dynamic routes.
- Tried 2 ways to disable prerendering for the dynamic routes. First, by adding additional entries in _svelte.config.js_. Second, by adding separate _+layout.js_ files next each _.svelte_ file. That still didn't help.



### Hour 21:

- Exploring _@sveltejs/adapter-static_. Looks like it's exactly what we want. Probably more.
- Explored [surge.sh]() in the context of hosting the build output. Generous offering.
- Switched to _@sveltejs/adapter-static_. Build failed saying that / was not marked for prerendering. So, I added a +layout.js with `export const prerender = true`. That triggered the prerendering. But, eventually failed with the error that some routes, specfically the ones with dynamic parameters were marked for prerender but could not be reached by crawling the website.

-----
<br>

### Hour 20:

Navigating to the deploy gives a plain _500 Internal Error_. Having some trouble trying to figure out the cause.
There's a similar Github issue that says this could be because of accessing filesystem on a serverless environment which
is unsupported. I didn't think I was using serverless with Netlify. But, when I checked, I found that a _Netlify function_
had been depolyed a few minutes ago. So, for whatever reason, Sveltekit's netlify adapter was deploying an serverless route for the build. Now, I'm digging to find out why.

Managed to check the function log. The issue is happening due to the @popperjs crap. I took a shot in the dark by removing
_vite.ssr.noExternal: '@popperjs/core'_ from the _vite.config.js_ with no luck. The bigger issue for me is the netlify function. I don't want to use them. I'd much rather just have a static deployment. But, it looks like _@sveltejs/adapter-netlify_ will create a 'render' netlify function as a rule for SSR.

I want to try _@sveltejs/adapter-static_ and see how that works with netlify. Vercel seems to have zero config support for that adapter and the same for netlify is forthcoming. But, I can't afford to wait for that. I need to figure out the configuration to deploy a static build on netlify myself. But, that has to be tomorrow. It's been a long 8 hour work day.


### Hour 18, 19:

Fixed npm scripts to build on netlify for production. Netlify build filesystems are case sensitive. That was producing some build errors. Fixed a tonne of file naming conventions issues due this canse sensitivity issue. Netlify build now successful.

### Hour 17:

Tested to see if the build is working as expected. Squashed & merged into _master_. Rebased _production_ and pushed to Github.

### Hour 16:

Took a hour long nap and it worked wonders. Got back and figured out what the issue was. It was a silent change in fabricjs API. Made the appropriate change and got the canvas working. Then fixed a couple of Azure config related issues.

### Hour 15:

Not even able to find a way to debug. Stepping through the JS code is becoming confusing because of all the Proxy objects and stepping inside fabric js. I need to take a gap, clear my head and try again.

### Hour 14:

No luck!

### Hour 13:

Installed _@sveltejs/adapter-netlify_ separately and got the build to work. But on testing the dev deploy, started seeing
some _fabricjs_ related bugs that shouldn't have been there. I figured it must be due to _fabricjs_ getting updated
inadvertently in the process of installing the netlify adapter. Trying to figure out a way to undo that and redo without
updating all the dependencies. Also need to reconsider the install step while building for production.


----
<br>

### Hour 12:

Looks like _vite_ dependency was updated. The recommended way to run the dev server also seems to have changed.
Earlier I was using _svelte-kit_. I'm not sure if that will work now. I also forgot to rebuild the container.
After rebuilding the container, I'm seeing error messages that make a little more sense now. It seems the build now breaks
because of lack of the netlify adapter. But that package must already have been included with _adapter-auto_ package.

Debugging further to see what's going on.


### Hour 11:

The migration guide recommends to update to the last version before 1.0.0 and test the app for better warnings. Being new to
_npm_ and _package.json_, it took me a while to figure out a way to update the _@sveltejs/kit_ package to specific versions.
Googling was painfully irrelavent. Finally figured it out. Before updating had to run `npx svelte-migrate routes` to update the routes to the new _+page.svelte_ convention. Then updated _@sveltejs/kit_ to _1.0.0-next.588_ which was the last version before _1.0.0_.

But unfortunately that breaks the build. Now debugging to see what the issue is. Error message is not too clear: _Error: Function called outside component initialization_ from loading the homepage.

### Hour 10:

I was checking the sveltekit migration guide and got distracted into exploring Gitbook for our tutorial content. Earlier I had setup _material-for-mkdocs_ on [learn.emptycup3d.com](). But, I was not fully satisfied with it. The entire site had a very 'tech' like feeling. Gitbook does what I need much better. Bigger, more friendlier font. Better space utilisation. Multiple page layouts. Custom domain support. It doesn't do a few nice things in terms of customisation. But that might not hurt us too much. Created a sample tutorials layout to test the view and [it was looking fine](emptycup.gitbook.io).


Anyways, this was not what I was supposed to be doing. But, I got sucked into it. Not too sorry about it though. Good find.

### Hour 9:

After making the config changes, the build succeeded. Then a few small changes to get the backend working without any runtime errors. But, it turned out that the frontend broke immediately after the first two pages. Svelte Kit has become stable and the entire codebase has been built on the development version before the major breaking changes that happened last year before 1.0 came out. So, the app was working on my dev machine. But failed right out on building on the server because npm pulled the latest version.

So, the next step is to move to the stable release of SvelteKit. I spent some time following up on the changes. Looks like the changes are not insignificant. This is already the 7th hour of _Deploy on emptycup3d.com_ which as estimated for 4 hours and I don't imagine Svelte upgradation is going to take less than 2 days. So, another 12 hours at the very least making a grand total of 18 hours for something that was expected to be less than 4 hours comfortably. Sigh.



-------
<br>

### Hour 8:

The issue was that a special character in the MySQL connection string was
messing up the formatting. Figured out a way around that after looking around quite a bit.
Now able to connect to the db. Initialized the tables.

### Hour 6, 7:

- Cleaned up _config_ for _emptycup.core_ by dropping *config_\*.py* convention.
- Fixed issues to get the change working in dev.
- Ran into an issue with not being able to connect to db for migrations on GH build action.
- Dropped `flask db upgrade` from the build process to bypass the db connection issue with no luck.


### Hour 5:

Fixing build issues on Github actions. *xxxxxx_options.json* conventions need to made consistent.
Further *config_\*.py* convention need to be dropped. That was a bad idea. Comparing config between different environments is a huge headache. Making a small change to config also needs to be made in 3 different files.


- Added Azure CDN for _emptycup3d_ storage account.
- Fixed store config for _prod_.
- Fixed db config for _emptycup.core_.

### Hour 4:

Decided to put off implementing `ec target production` and getting _eccli_ to run from dev machine atleast till after the deployment. Added tasks in tracker.

Merged into production branch and pushed. Github repository secrets are missing after downgrade from Team plan as Organisation secrets are not supported in Free plan.

Turns out, I cant push without merging changes from fixing the AssetStore. Have to now clean up _furnishings_ branch and merge it with _master_ and _production_ to proceed.


### Hour 3:

Explored duplicating the production db to "beta". Turned out too complicated. Decided to name db as _v2_. Not too sure of long term implications on convention.

Updated production config: db, redis. Unchanged since before Azure migration about 4 months ago

Moved deploy changes to a different temporary _deploy_ branch. Merged those changes with _master_. But, _master_ and _furnishings_ have now diverged. Created a _v2_ database on the production server, but the tables are not created in that db. To do that right, I need to make `ec target production; ec db reinit`. That is going to be some work :'(

Before doing even that, I want to get `ec` working on my dev machine rather than the container. Not sure whether I have time for that. Better to db reinit from the container after deploy and then come back and implement this after that.

-----
<br>

### Hour 2:

- Reviewing monthly goals.
- Updated expectations for this quarter.

### Hour 1:

- Finished last week's review.
- Finalised plan for coming week
    - Deploy on [emptycup3d.com]()
    - Enable paritition delete
    - Enable move control for ledges
    - Fix modular design page scroll
    - Fix material application
    - Setup render workers
    - Fix white default materials @ _studio3d_
    - Fix UV scale for wall textures in 360


-----
<br>

I spent the last week importing the furnishing and material catalogues. Almost done with that work.
This week's focus is to publish on [emptycup3d.com]() even with issues.

Apart from that, I will also be mindful about my own productivity. A few mental notes in that regard:

- Whenever feeling low on creative energy, reduce the intensity of work, but don't give up.
- A few tips for low intense work:
    - Pick up a different easier, smaller task on a different branch. Make sure there's not more than 1 such branch open.
    - Do some house keeping work: documentation, comments, task tracker, FIXXXME.
    - Write something: strategy, plan, tutorials, product etc
    - Work more slowly and methodically. Tie a bow.
    - Become more verbose on the devlog.
    - Keep a pen and paper to break down complexity of the task.
    - Break time into smaller "periods", preferably 20min.
    - Take a short 10-20min walk and get back.

- A few tips to reduce complexity of the work:
    - Take more time to plan the work.
    - Break down work into clearly definable tasks.
    - Take more time with pseudocode.
    - Take smaller steps with closer checkpoints.


The goal for this coming week is 40 hours. This week I have to log the hours as well, no matter how pedantic.