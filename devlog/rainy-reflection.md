---
layout: page
title: Rainy reflection
---

An aimless reflection of a 3 week period in the monsoons.
There are a lot of things that I want to consider deeply.
 - A random sampling of my work load.
 - My drive over a considerable time chunk.
 - Understanding priorities at a higher resolution.
 - Compulsive need for busy productivity.
 - Loss of intensity in the middle phase of a sprint
 - Gaining elevation coming off of a minor trough.
 - Variation of energy levels with weather.
 - Challenges in building & managing an intense routine.


---
<br>


### Day 1:

- Regrouped on priorities.
- Switched to working on pepper, a chrome extension to automate browser tasks.
  Exploring ways to automate image generation on chatgpt.
- Planning to start on rate card import.

Saw that the offline support was not deployed.
So, decided to wrap that up first. Pushed to production.
Not working as expected. Reverted.
Spent a couple of hours trying to figure out what the issue is.
Fixed a couple of production specific issues that didn't show up in development.
Still it is not ready. Will pick it up again tomorrow.

Fixed an issue with `podium`. Signups were getting blocked. It was a firebase rules issue.
Added some permissions on facebook ads manager. Added funds for the account. Had a quick call with Viswanandh.

> One of the traps that I keep falling into is not having a sharp closing.
> Whenever I run into days like today when things don't go my way, ugly code or stubborn bugs,
> I have a tendency to drag work beyond closing. It's like a false hope or unwillingness to accept
> the overhead cost of context switch or reluctance to readjust my own expectations.
>
> It wouldn't be such a big problem if it were just that disturbance.
> It spills over and ruines the rest of the day or routine and spoils the rhythm.
> It leaves a bitter taste to the days and ends up taking a lot out of drive.
> The worst part is that even when I extend, that issue rarely gets resolved that day.
> So, no result and you end up screwing up the routine for the day.
>
> And the surprising thing is, whatever was so annoyingly sticky gets fixed in 5-10min
> the next morning. I have let myself fall prey to this miscalculation quite a few times.
> There's definitely some deeper insight here for me learn and internalise.
>
> May be respecting time. May be detaching from result. May be respecting the bugs.
> May be preempting such frustrating sessions proactively (may be even aggressively falling back)
> May be managing my own expectations? May be keeping the bigger picture more closely in mind...

This left a pretty bad taste today as well.
I was pretty geared up for the week.
Planned to work on a completely different task and this issue which I had written off as done,
popped up again and took as much time as the original implmentation.
I was only able to find my peace after my daily meditation.
It shouldn't be like this.


### Day 2:

Continuing from where I left off yesterday.
Before I get started, it seems my fiddling with the beta version seems to have had side effects.
Got an notification from the team that they have been facing issues with beta since yesterday.
I had even pushed the same branch to production. On production, there has been an instance of renders failing.

I should probably, have a short session to continue the offline debugging on beta.
In the afternoon, I need to take a look at the renders issue on production.

The offline issue got resolved quickly.
I cleaned up and refactored the implementation.
There is still one small glitch with the loading icon not being properly cached offline.
I did spend a half hour over it.
I'm eager to finish it off even if it means an extension post lunch.

> These are the kind of decisions that I find myself questioning often.
> Fixing that issue would not impact functionality. Only the overall polish.
> It is something that can be written off as a polish, though it robs the feeling of elegance for a user.
> I question my prioritization with such issues.

Post lunch was painful. Same story today.
I couldn't give up that issue for fear that it might lead to a bigger issue in production.
But, unfortunately, it eluded day 2.

Resolved a few things wrt to the sales pipeline before wrapping up for the day.


### Day 3:

I figured out the root cause of yesterday.
I seems to be a completely unexpected detail. Fixed it.
Fixed a couple of other glitches caused by the same issue on deploy.

On deploying, found a bunch of other corner cases that needed to be addressed.
The main cause was that on production, the frontend and backend are on different domains.
Whereas in development, both are on localhost. Hence the behaviour of the cache needs to be updated.
Fixed all those issues.

Made some fixes on podium.
Added some of the missing videos.
Reviewed some existing content and checked the analytics.
It didn't look exciting on first glance. Looks like it will still be a slog.

_Overall, another slow day._


### Day 4:

- Fixed an issue with course contents not loading on first load.
- Verified that offline support working without glitches on beta deployment.
- Shared detailed feedback on the presentation for `Why design first...` lesson video.
- Added address and phone number to the contact form
- Added google maps embed of office location
- Integrated the contact form with google chat on submission.
- Added poster for the introduction section on the landing page.
- Course content uploaded on Netlify was buffering repeated.
  Switched to Azure Edge, though I wish Netlify could handle such basic stuff.
  Need to evaluate if this is a netlify issue or if there's something else going on.

Fix: Minor issues with offline support
  - Removed embarassing error reporting
  - Added explicit condition to cache select pages as well
  - Fixed bug with reloading render tour on save

There still seems to be some issue with the implementation as the page
sometimes claims that the model has been updated. This seems to be a consequence
of bypassing the cachebuster params on the woodwork and layout update requests.
I need to dig deeper to verify and validate this. Will get to that tomorrow.

Had a call with a client and then the marketing team. Both productive conversations.

_Considerably more productive work day today._

> I need to figure out how to reorient my internal sense of progress & productivity
> so that I don't get effected by these ups and downs of work. It takes an emotional toll
> when you have a few bad days in a row. At the same time, the good days aren't completely
> due to my own doing. Focusing on the process more than the destination gets harder and harder
> as the going gets tougher and tougher. I'm still trying to figure how to make that change
> in my perspective. It doesn't feel like something that insight can address. It probably needs practice.
>
> Culture is very much a product of leadership. The broader implication here is that this conflict
> percolates slowly into the team as well. I have seen a few instances of that too, though it is much
> easier for me to call it out and pacify the team. But, pacifying myself on the bad days is much harder.

### Day 5:

Started the day by putting together a dashboard to track our marketing activities.

I feel like I need to have some momentum and clarity before I can handly and content activities.

> This idea of choosing tasks based on their demands and my current state needs more thought.
> There are some tasks that need explosive energy. Some that need a kick start. Some that need patience.
> Some that need a lot of attention to detail. I have noticed that if I pick a task that doesn't match
> my current energy level, focus level, it ends up taking a lot of energy. Conversely, if I pick up a
> task that matches my "gear", it gets done easily. There is huge leverage for taking if this notion
> can be understood more deeply and work planned accordingly.

For now, I don't feel like anything creative. I feel like picking up something that takes attention to detail
and analytical effort rather than creative efforts. So, may be a good time for implementing the ratecard import.

The layout getting reset issue on beta is also a danger. Probably that needs to be addressed first.
But that one feels like a bit unpredictable and could be potentially frustrating. May be better picked up with a
fresh mind tomorrow.

Switched to `claude-sonnet-4`. Took an hour and half to describe the ratecard import logic.
Implemented a CLI command `ec ratecard convert` to convert a `.xlsx` to `.json`.
`claude-sonnet-4` is pretty impressive. It asked the right clarifying questions.
Seems to have implemented smoothly. That was a good experience.
The implementation is still a few steps from being merged though.

I was expecting this to take a week. So, pretty happy with today's result.

### Day 6:

Shelving the ratecard conversion branch temporarily.
Picking up the issue where the layout gets updated due to cache buster param issues.
Turned out the cache busters were not the issue at all. It was the browser referrer policy.
Getting around that was lot of back & forth. For different asset types, different requests and different environments.
This is really sticky stuff.

> It was the right call to avoid this issue yesterday.
> Would have drained all the energy without a positive result.
> I underestimated the inertia of this thing even today.
> Also committed the earlier sin of breaking time limit for the day.
> I got frustrated and turned stubborn. Felt like stabbing someone midway through.
> But managed to keep my calm and try again. Luckily I managed to get a breakthrough.
> The battle is won, but the war is not over on such issues.


### Day 7:

Added support for explicit caching for offline mode. Nasty stuff.


### Day 8:

Reviewed mixpanel numbers. A few immediate changes needed. Started working on those.

- Implemented user identification
- Implemented tracking user profile
- Refactored firestore implementation

Had a call with Kanishk to review lead quality.
Decided to prioritise the change in flow to prioritise booking over course.

- Setup claude code.
- Implemented a booking first flow that excludes the course
- Worked out data tracking using calendly

> Good day today. Felt like high priority, high leverage work.
> A welcome change from wading through that swamp.


### Day 9:

Was taken over by bug on production for very high end projects.
Sat debugging that the entire day and late into the evening.
The issue did not get resolved even then.
Managed to provide a temporary workaround for a few days of relief.
Will have to get back to this very soon.


### Day 10:

Got back to the highest priority issue: Increasing call bookings.
Redid the website for a booking first flow.
Claude is pleasant to work with. I haven't had a bad experience yet.
Got the ad variations ready.
Reviewed the v2 of the opening videos for the landing page & the course.
Redid the voice over for one of the opening videos.
Redid the ending for the intro video to change the CTA.


### Day 11:

Deployed the updated videos.
Deployed the booking flow.
Had a call with Surya to explain the ad creative strategy.
A lot of website polishes and improvements in copy.
Created an "impressive" /booking page.


### Day 12:

I want to spend a good chunk of time on the core product now.
The 3 main angles that I need to shore up are: onboarding, devops & production.
There's no way I can make any reasonable headway with any of those directions
in the short amount of time that I have.

Trying to leverage Claude to parallelise & automate.
Just issue description and fleshing out an implementation is a big deal here.
Got claude to come up with first description.
Setup a md file based workflow for iterating on implementations in parallel.
Fleshed out a few issues in depth.

> It feels truly liberating fleshing out issues for AI.
> Thanks to the computing god(s?) for blessing me with such powers at this point in my life and work.


### Day 13:

Spent a couple of hours fleshing out 20 issues.

The initial description that Claude came up with are totally useless.
It feels like ChatGPT can probably do a better job at this. No code context whatsover.
Iterating on github issue creation workflow with claude. Managing with .md files for now.

Got claude to outline the implementation. That prompt needs to be refined much more.
Even after my nuanced description of the issues. The input added by claude is very minimal.
Failed to catch any insight in the outline phase.
Infact, there were a few blunders that I chose to overlook.

Decided it would be easier to refine the outlining flaws if I got a sense of how
well the implementation goes. I might be able to infer patterns on where it does poorly
and update my outline prompts to bring out those issues. So, let it rip and off it went.
Had to give a few permissions and couple of nudges midway before it finished.o
Will dig into those PRs tomorrow and evaluate the first round results.


### Day 14:

Fix CORS
  - Did not have allowed domains in config.py
  - Unnecessary verbosity in logging
  - Unnecessary function definitions in api.py (get_allowed_origins) even on refactor
  - Bad choice of default behaviour (falling back to development config, further falling back to [])

Thin Woodworks
  - Completely broken implementation

There's no point documenting this. It was a complete disaster.
Claude's understanding was extremely superficial and it failed irrecoverably.
One possibility could be that asking it to implement issues in a single thread caused this (unlikely).
Another issue could be that the issues need to be fleshed out a much lower level.
Better prompts would be able to help with this. A more involved workflow would do better.

I'm cleaning up some old PR and putting together a sprint branch for release.

### Day 15:

Worked on a few issues myself today. For eg: Bulk customisation: Had to completely redo. But to be fair, the issue turned out to be more complex that I had thought.
Still reviewing AI's v2 implementation for async fetch assets for render worker.
Merged a couple more PRs into sprint for release tomorrow.

I'll have to regroup and prioritise tomorrow.


