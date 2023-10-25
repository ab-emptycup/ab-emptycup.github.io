---
layout: page
title: Product - October'23
---

This log is commencing only in the last week of October 2023.
There is probably 5 days of work left. I'll be taking up this thread at a leisurely
pace as this is not my highest priority this quarter.


### Day 1:

This week's agenda is to establish a firm working context again. 
I'd recently committed to a system factory reset that cleaned up the dev environment.
In my experience, doing this periodically has been beneficial. It aids in improving
the working environment, but comes at the cost of extra investment in setting up 
the environment again.

- Added basic shell aliases
- Recreated SSH keys for Github
- Setup vscode editor with basic extensions
- Cloned and setup the work and log repositories


### Day 2:

Started working on setting the dev deployment for emptycup3d.

- Installed dependencies
- Installed docker
- Updated instructions in README.md
- Got the docs to deploy on localhost
- Fixed issues with running docker containers for Mac M1.
- Got the webapp, db and redis server to deploy

Ran into an issue with the api server where the supervisor service was failing to create a socket.
This is very likely due to some path not existing or not having the right permissions. I tried 
seeing if I could quickly resolve this, but I couldn't. So, I'll take a shot at it again tomorrow.
I got the webapp to deploy properly and could load the landing page on the browser.


