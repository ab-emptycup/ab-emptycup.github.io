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

Made some fixes on podium.
Added some of the missing videos.
Reviewed some existing content and checked the analytics.
It didn't look exciting on first glance. Looks like it will still be a slog.

_Overall, another slow day._


