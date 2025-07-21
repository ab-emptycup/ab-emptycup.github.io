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