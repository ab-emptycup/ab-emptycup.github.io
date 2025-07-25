---
layout: page
title: AI Assist
---

Rebooting on engineering to level up. Will do an hourly log without an agenda or an expectation.
Let's see how far this goes.
My focus for this log is level up our AI game for product development (mostly).

Here it goes...


### Hour 1:

- First I need to regroup on the status of the repo.
- Then clean up the environment (dead branches, stashes etc)
- Then I need to figure out what are the things that I need to work on.
- Then I will explore what I can do with AI get a leg up.

`compinit` zsh issue because of homebrew on multiple user accounts [Fixed]

Quotation functionality not working. Everything showing as zero.
- Looking into that. Will probably start refactoring & cleaning up implementation.
- The implementation is just Uhhh gleeee. 1300 lines in the page component. Feels like java.
- **Asked copilot to add console logs and boom I can follow execution in the browser console. Neat trick.**
- Tried resetting the quote with no lukc.

Next I want to first get it to work as expected before refactoring.


----
<br>


### Hour 2:


**Found out that copilot cannot make edits if the code is folded. WTF!**

The issue is with the local storage backup functionality.
When requesting quotation for new projects, it gets computed properly.

The code is unbelievably ugly. I actually feel nauseated.
I feel this strong urge to kill someone when I read it.

I duplicated the `/quote` page into `/quotation` so that I break it apart and refactor.
Sveltekit is acting up by suddenly giving 404 for `/quotation`. Tried cache refreshes.
It worked once when I tried to reboot the container.
It worked once again when I rebuilt the containers from scratch.
This kind of unreliable dev setups are really frustrating (on top of the ugly code from juniors).


---
<br>

### Hour 3:

- Replaced the /quote to bypass the sveltekit issue
- Separate js and css from the quote generator page

Copilot is really slow on our repo because of .gitignored `data` and `logs` folders (presumably).
I checked if there's a way to exclude them. Only available for Business Organisations & Enterprises.
That sucks.

Started refactoring.

---
<br>

### Hour 4, 5:

Cleaned up a major portion. Copilot helped with some big changes in the beginning.
As the changes got smaller, it didn't make sense.

---
<br>

### Hour 6, 7:

The entire implementation has been a complete shit show.
I'm torn between having to rewrite it and cleaning it up.
The challenge with rewriting is the UI part.
The more I think, the more I feel this is a lost cause.

---
<br>

### Hour 8, 9, 10:

Decided to continue cleaning this up normally.
Rewrite would have been much easier especially with AI.
There are thousands and thousands of ugly duplicated code.
_One major learning for me is that AI in the hands of imbeciles can ruin a codebase._
The worst part is that AI can't help with clean up.
It takes other ugly parts of the code as inspiration.


---
<br>

### Hour 11-14:

Going on and on...
At this point this is not even a good engineering session, let alone AI assist.

---
<br>

### Hour 15, 16:

My entire local db just vanished out of the blue.
So strange and a bit scary.
The database is empty. Not sure what went wrong.
Must have something to do with the docker container build.
Didn't feel like digging into it. So, got a db dump from beta and imported.

Continued the refactoring.
- Managed to get a price calculation to show for woodworks.
- Units & LineItems not showing yet.

---
<br>


### Hour 17, 18:

- Got Units to show
- Got Dimensions to show
- Dimensions are now editable.

Cursor AI has been quite helpful.
_It seems the key is to define what is expected in a very detailed way._
Lazy explanation and hoping AI will figure out isn't doing the trick.
Typing in English is definitely less draining that typing code.
But it does still force you to think in a pretty detailed manner.


### Hour 19:

Starting to get a hang of Cursor now.
Got it to implement the entire `Customisations` component.
It did a pretty good job to be honest.
_The key is to define the requirement very clearly._
I think what led me astray so far is the small prompt box in the UI.
You kinda default to small prompts with that UI.
Instead I added a new folder `issues/` and described the functionality there.
Then used that as a base to add more and more context.
I used the `Ask` mode to take the description and generate the plan for an incremental implementation.
This is fun!

### Hour 20, 21:

- Got price updates working
- Fixed an issue with styling
- Got inclusion working
- Got dimension updates working

### Hour 22:

Got the header working
I need to make some change in the way I work to leverage AI.
Right now, I'm only able to take help when the changes are significant.
Otherwise, I'm jumping in and making the changes myself.

### Hour 23, 24:

Got the Settings modal working
Apart from minor glitches and slip ups, starting to get a hang of Agent mode.
Really enjoying it.


### Hour 25, 26, 27, 28:

Tried to get add items to work.
Was a bit slow while multitasking a few things.
Was able to quickly figure out the boundaries of AI.
Tried to give it a broad description of functionality.
It did manage to deliver step by step. But got quite a few things wrong.
_So, its not about depth at all. It is about parallelism._
The obvious next step for me to try would be to let it break down the
implementation without making the changes and list it in text.
Then I can offer corrections in one shot instead of trying to discover its implementation
after it makes changes. That part is expensive in terms of my time.

_Plus cursor is drinking token credits._
I will have to work out techniques to minimize that.

Even so, it is still a good deal compared to the output from the interns.
On second thought, is it though? If we can find them, good interns are 5-10k per month.
Best case they have a 1:10 return on my time. Their through put is may be 10x slower than AI.
So, Output(1 hour of my time + 10 hours of their time) = Output(1 hour of my time + 1 hour of AI)
Their month is 100 hours. So 50-100/hour. So, 10 hours is 0.5-1k.
Right now AI for is at about 150 per hour. So, yeah 3-8x better.


### Hour 29, 30:

I had tried to push the AI a little bit yesterday by defining the problem statements
at a slightly higher level and that caused a lot of collateral damage.
It was very unclear whether to dump the entire change or make corrections.
Just cleaning up a few things and getting the basic to work again took 2 hours.

1. _Making AI do fuzzy things causes a lot of havoc_
2. _Making AI edit an unclean / unorganised codebase is a bad idea._
3. _Always. Always. Take the time to solve the problem logically first before asking AI to implement._
4. _DO NOT get into the muck of cleaning up AI's work. That's the opposite of leverage._


### Hour 31, 32, 33:

Wasted some time trying to fix things, before realising bigger modules need to be rewritten.
The `Dimension` component which was just a small input box was becoming too complicated.
Finally decided to flesh out the requirements and just the untangling the complexity took 30min.
AI did a decent job of implementing when the changes were so clearly defined.

### Hour 34:

Started fleshing out the requirements for another key module which is the data model for managing `units`.
That started gathering a lot of complexity and needed to be simplifed and clarified. Midway through that.

This has been a very disappointing week. On reflection, the root cause for this is the ugliness
created in the existing code. I think I would have been faster and happier if I just dumped the old code
and started from scratch.

Frontend styling is still a weakpoint for me which caused me to avoid the rewrite from scratch.
I'd rather figure this out than figure out frontend. But I hear AI is built for such dumb problems.
May be some other day.



