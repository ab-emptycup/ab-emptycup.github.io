---
layout: page
title: Jan Week 3
---

Jan 15 - Jan 22<br>
Week#: 3/52<br>

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