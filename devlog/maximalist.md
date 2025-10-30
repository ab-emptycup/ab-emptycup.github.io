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


---

- ~~Setup --dangeriously-skip-permissions~~

- ~~Got a production issue at 3 in the morning. Turned out to be a race condition in project save. Patched it.~~
- ~~Test yesterday's project import script~~
- ~~Browser based auth flow is incompletely implemented.~~
- ~~Got a new production issue in the afternoon where 2D drawings are not being exported.~~

- ~~Investigate issue with 2D drawings using only the top left quadrant~~
- ~~Fix the device dependent 2D drawing rendering issue~~
- ~~Investigate the efficacy of the 2D drawings~~
  ~~Fixed a nasty bug after 2 hours of iterative debugging.~~

- ~~Rewired yesterday's course flow to capture visitor's profession and projects per month.~~
- ~~Test the flow locally and add documentation~~

---


Cleaned up CLAUDE.md and set it up for all repos at ~.
Added detailed code style guidelines. 


---


Shaping session:

- ~~Refactor of WalkinLoader~~
- ~~Cleanup of old render workflow~~
- ~~Principled BSDF Implementation~~
- ~~Render tuning framework~~
- ~~Azure blob storage to Cloudflare R2 migration~~
- ~~Project backup & restore~~
- ~~Theme duplication along with project~~
- ~~System wide credential rotation~~
- ~~Alias cleanups in shell configs~~
- ~~Rate limiting for API~~
- ~~Community catalogues~~
- ~~Catalogue favourites now persisit in DB~~
- ~~UI for ratecard editor~~


---


- ~~Remove AGENTS.md & .cursor folders~~
- ~~Setup CLAUDE.md~~
- ~~Setup worktrees again (properly this time)~~
- ~~Setup a /tutorials page~~
- ~~Investigate issue with quote composition~~


---


- ~~Setup Skills~~
- ~~Cleanup superpowers~~
- ~~Resolve the quote composition issue across projects~~
    - ~~Resolve issue with local project import~~
    - ~~Fix expired token server error~~
    - ~~Fixed the semantics of the unit level pricing switch~~
    - ~~Pricing level can be switched from quote page itself~~
    - ~~Improved the styling of the project settings modal~~


---


- ~~Setting the stage for v3 release:~~
   - ~~cleaned up feature branches~~
   - ~~rebased beta & master~~
   - ~~developed a pr-review skill~~

- Reviewed: API Ratelimiting
    - ~~Fixed a bunch of issues in code~~
    - ~~Redis config not handled properly~~
    - ~~Server not setup properly~~
    - Looks like base container image needs to be updated
    - That would require assimp updated
    - That could break the furnishing flows
    - Need to setup the test suite
        - ~~Wrote the implementation plan for an e2e test suite~~
        - ~~Implement the plan and debug test suite~~
        - ~~Fixed issue with auth for tests~~
        - ~~Fixed issue with database connections~~
        - ~~Gave directions to claude on how to iteratively navigate the app & update tests~~

```

⏺ Task(Fix test_furnishing_library.py)
  ⎿  Done (67 tool uses · 140.9k tokens · 19m 48s)

⏺ Task(Fix test_material_catalogue.py)
  ⎿  Done (38 tool uses · 69.3k tokens · 18m 0s)

⏺ Task(Fix test_material_duplication.py)
  ⎿  Done (30 tool uses · 59.8k tokens · 13m 16s)
```



---

Test suite implementation:
 - Current implementation is a mess.
 - CC has been struggling since yesterday morning.
 - Took multiple shots at making it stable. But far from ready.
    - Failed tests
    - Unreliable tests (race conditions & timeouts)
 - ~~Got a simplified single regression test (with 9 test cases working)~~


Meanwhile, there are a few production issues that need resolution:

- ~~VSL based registration flow on Podium~~
- ~~Ratecard upload bug on beta~~
- Resolving the line conflict from ratecard (for matching categories)


----

- Develop /shape
- Explore #memory
- Explore Amplifier

- Review and merge the pending PRs
    - Iterate on the PBR tuning framework

- Brainstorm pending issues:
    - Creating concept renders
    - Composing modules & quote integration
    - Fixing the existing test suite
    - Complete code audit
    - Fixing docs
    - Blob encryption
    - Curved ledge design & composition

- Test the material application issue on beta
- Investigate the wall composition inconsistency

- Remove side effects for tests in Gong
- Setup Sendgrid and integrate in dev
- Setup WhatApp API and integrate in dev
- Draft a test drip definition file
- Shape & implement Gong API authentication
- Brainstorm and develop course retention drip messages
- Deploy on Azure
- Integrate with Podium






























