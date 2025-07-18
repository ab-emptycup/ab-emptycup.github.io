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

