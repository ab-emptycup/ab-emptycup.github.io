---
layout: page
title: AI Maximalist
---


 - ~~Cleaned up and rebased all PRs. Feeling a little better now.~~
 - 




 - Show login succeeded in browser for `ec login prod`
 





---



  - ~~Need to rethink how the test data is tracked (git lfs?)~~
  - ~~Need to rethink the way tests include frontend code.~~
  - Need to figure out a way for UI component testing.
  - Need to bring the test recorder for E2E testing.
  - `ec projects save --from beta/prod <pid> <pjsonp>`
  - `ec ratecards validate <xlsxp>`
  - Update config.py to create rootdirp relative to file
  - 



---


I'm clearly getting overwhelmed by multi tasking.
I think I'll be way more effective if I just did single tasking and don't care about driving AI. 
It feels like in the pursuit of driving AI, I'm losing my way.

- ~~Unable to see customisations for tandom box~~
- ~~Handling open boxes & tall units intelligently~~


Simplified my approach. Instead of trying to design a test suite for the entire codebase,
now I'm just focusing on the ratecard and quotation flow. This is itself is a big deal.
It seems even this small subproblem still carries a lot of that architectural complexity.



---



- Assets are taking time to load after offline support

- Code review / Code polish agent
    - ~~Write a skill by hand myself~~
    - ~~Bootstrapped the skill with TDD Skill builder~~
    - ~~Tested it against a live PR~~
    - ~~Revised it for more rigourous checking~~
    - ~~Mega Polish: Ran the skill on the entire codebase~~



- Add `note edit <id>`



---


- Reorganised all the docs
- Cleaned up old out-of-date docs
- Setup AGENTS.md with guidelines for writing docs
- Rewrote all the docs as per the guidelines
- Reorganised all the ai implementation plans
- Fixed the skills to respect the new conventions
- Fixed aliases to avoid dumping pages of AI plans in diffs

Hard to believe what a big difference that cleanup has made on my psyche.
I feel so much lighter in the head. I'm actually excited to build further.


---

- Should I complete the lean test suite?
- Should I get the work started on the large test suite?
- Should I continue reviewing more PRs?
- Should I setup the PR review tooling?
- Should I merge pending PRs?
- Should I kick off the PBR thread?
- Should I integrate a simple test suite?
- Should I start work on v3?


What's urgent and what's important?
    - Nothing blocking right now.
Ok, so its not about urgency then. What then?
    - Not sure where to get started.
May be its time to get organised a little. 
    - The v0 tests are already in master
    - v1 tests will take time 
    - v1 tests might exhaust claude credits
    - codex has already been exhausted
Can we move forward without test suite then?
    ...forward to what?
Either merge existing PRs or v3?
    - Definitely feels like clean up and v3
    - But that might disturb the environment too much.
    - ~~First starting to clean up my system~~
        - Running out of memory too often
        - Running out of storage space too often
            - Freed up 70GB
        - CPU hits 100% regularly

Started by cleaning up the docs. Better get started than think about it.



---

Deploy quotations v3
 - ~~Get db backed quotations ready~~
 - Review & test ratecard sharing
    - ~~The PR was so messy that I started fleshing out the requirement again~~
    - ~~Consider moving `Ratecard.name` to `Account.ratecards`~~
    - ~~Kick off reimplementation~~
    - Looks like the quality of code is still pretty poor



PR review and code polishes are taking *A LOT* of time.
Though I think there's a way to streamline with proper tooling, the current setup is painful.
It is taking almost as long for pr review with AI as it would manually. Probably even a little more.
Here's what I have in mind to address this:
    - a structured pr review skill
    - a structured code polish subagent


Merge the test suite

Setup Gong to engage new registrations on website


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


---


- ~~Add credits to KaaS~~
    - Verify admin access to add credits
    - Add Dilpreet as an admin

- Merge the /quotation related PRs
    - ~~Ratecard import validations~~
    - ~~DB backed quotations~~
    - Ratecard sharing
    - ~~Show validation message on rate card upload~~

- ~~Flesh out a leaner test suite~~
- ~~Get codex to write the tests~~

- ~~Deploy the VSL flow~~

- ~~Implemented a cli tool `note` after losing a 30min prompt on claude~~
- ~~Implemented a cli tool `hn` to summarise and filter hacker news to test codex~~

----

- Started designing a test recorder + player module
    - ~~Create an detailed implementation plan~~
    - ~~Implement the plan & create PR~~

- ~~Outlined a comprehensive test suite~~
    - ~~Got CC to flesh it out in detail: 9000+ tests & 4000+ checks~~
    


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


- ~~Setup Skills~~
- ~~Cleanup superpowers~~
- ~~Resolve the quote composition issue across projects~~
    - ~~Resolve issue with local project import~~
    - ~~Fix expired token server error~~
    - ~~Fixed the semantics of the unit level pricing switch~~
    - ~~Pricing level can be switched from quote page itself~~
    - ~~Improved the styling of the project settings modal~~

---


- ~~Remove AGENTS.md & .cursor folders~~
- ~~Setup CLAUDE.md~~
- ~~Setup worktrees again (properly this time)~~
- ~~Setup a /tutorials page~~
- ~~Investigate issue with quote composition~~



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


Cleaned up CLAUDE.md and set it up for all repos at ~.
Added detailed code style guidelines. 



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


-----

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

























