---
layout: page
title: AI Maximalist
---

There's a lot to be done.
The purpose of this log is to add some weight and friction.
Ideally, I should be able to skip this log as much as possible.
Whenever I feel overwhelmed by multitasking, I'll keep coming back here.
I'm working on 3 repos mostly: gong, emptycup & podium.

## Gong
 - Setup sendgrid test and whatsapp api integration
 - Deploy on azure functions and run remote e2e tests
 - Shape & implement auth

## EmptyCup
I need to get organised and power up first.
 - Setup claude?
 - Setup /shape?
 - Design & implement tests?
 - Fix production bugs?
 - Explore Amplifier?

## Podium
 x Setup skills for cursor? gemini?
 - Revert to the course flow, but with the /booking page

I'm stuck here:
 - Setting up skills for Gemini or Cursor feels like a big task
 - Setting up sendgrid & whatsapp api feels like a boring task
 - Developing /shape also feels like a big task

I guess this is the danger of working with AI.
You gradually lose the capability to pay attention to detail and dig in.

Ok setting up skills will take some time. Not for now.

- Fleshed out the new course flow for Podium using claude 
- Developed an implementation plan and handed over to Codex
- Setup Gemini to evaluate efficacy.
- Used Gemini to implement a script to backup archived github repos
- Backed up and removed the archived repositories (all 89 of them, wtf!)

Shaped an incremental backup script for security.
Setup a dark vm and ran the backup script successfully.
Need to make some polishes for deploying as a cron job.

Rethinking the ideal course flow. Not too happy with it right now. 
That turned out to be more complicated than I expected.
There is no complexity. Just a lot of tiny complications.
Fell back to CC to brainstorm and flesh out the tasks.
It's gone off to implement those tasks now. Let's see how long it takes.

I want to get started with the emptycup3d repo in parallel.
Started shaping a project import script to pull prod projects into dev environment.
Critical for debugging. The shaping process took over 30 min.
CC developed a detailed plan is off implementing it.
Meanwhile...

The course flow changes got blocked a couple of times and finished in 30min.
There were errors with firebase rules. CC patiently got those issues resolved with my help.
Realised a loophole in our migration process. Now implementing an admin sdk script to migrate properly.
Ended up taking a lot of attention. I shudder to think what I would have done without CC.
CC did most of the heavy lifting. After more than 2 hours of to and fro, flow looks good.
Fixed a few other issues as well from before.

CC reports success after about an hour on project importing script.
Apparently tests are also passing which is very very unlikely.
Probably some dummy 1+1 == 2 kinda tests. Will have to explore tomorrow.

Massive backlog on product.
Quote generator. Production fixes. Security patches. Optimisations. Cleanups. High demand features.
Haven't even touched Gong today. Deploying that will be the priority tomorrow as the v3 website flow is ready.
Good times!


## Day 2:

[x] ~~Setup --dangeriously-skip-permissions~~

[x] ~~Got a production issue at 3 in the morning. Turned out to be a race condition in project save. Patched it.~~
[x] ~~Test yesterday's project import script~~
[x] ~~Browser based auth flow is incompletely implemented.~~
[x] ~~Got a new production issue in the afternoon where 2D drawings are not being exported.~~

[x] ~~Investigate issue with 2D drawings using only the top left quadrant~~
[x] ~~Fix the device dependent 2D drawing rendering issue~~
[x] ~~Investigate the efficacy of the 2D drawings~~
  - Fixed a nasty bug after 2 hours of iterative debugging.

[x] ~~Rewired yesterday's course flow to capture visitor's profession and projects per month.~~
[x] ~~Test the flow locally and add documentation~~

## Day 3:

[ ] Setup Skills
[ ] Cleanup the superpowers plugin
[ ] Develop /shape
[ ] Explore #memory
[ ] Remove AGENTS.md & .cursor folders
[ ] Explore Amplifier
[ ] Setup worktrees again (properly this time)


[ ] Test the material application issue on beta
[ ] Investigate issue with quote composition


[ ] Remove side effects for tests in Gong
[ ] Setup Sendgrid and integrate in dev
[ ] Setup WhatApp API and integrate in dev
[ ] Draft a test drip definition file
[ ] Shape & implement Gong API authentication
[ ] Brainstorm and develop course retention drip messages
[ ] Deploy on Azure
[ ] Integrate with Podium


[ ] Setup a tutorials website using the available tutorials on `learn.emptycup3d.com`






























