---
layout: page
title: Rewriting modular.js
---

_modular.js_ is EmptyCup's woodwork design interface.
This is a log of it's rewrite as part of total product rewrite.
<br><br>

### October 31:

I'm trying to get the component move to work. A few considerations:

- Component move should show a shadow moving with the pointer.
- Undo should set the state to before the move was initiated.
- Move should snap to all the relavent snap points.

It has been a week since, I last looked at the code. So, there's has been a context reset. I don't think I can get up to speed and make changes in just 2 hours. I'll work on something else today and start off tomorrow.

---
<br>

### November 1:

1. First step is verifying that the existing setup is stable and working.
2. Then, I'll make the shadow appear and move instead of the actual component.
3. Then, I have to figure out how to identify all the viable snap points.
4. Then, I have to actually move the component onDrop.


TODO: I'm not clear on how docker's storage/caching works. I need to learn about it. I'm inadvertantly deleting containers and rebuilding takes quite a bit of time.


Gumption trap early in the day. I had deleted my dev containers earlier.
Now when I try to rebuild, it suddenly starts complaining that the platform
 'linux/arm/64' is incompatible with mysql which is true enough.
Earlier, I think I was passing a platform flag to docker to emulate 'linux/amd64'.
But the right fix for this is to use mariadb which seems to be a drop in replacement.
So, I do that. There's some issue with mariadb getting started:
Could not figure out what the issue was. So, decided to continue running docker in emulation mode 'linux/amd64'.
Some strange behaviour noted. But, don't feel like digging into it now. I'll leave it with a mental tab.


- Got the shadow working and moving along with the pointer. Then the component moving with a jump on drop.
- Snaps are still not working.
- Noticed an issue with shadow being orphaned when the pointer leaves it.
    - Likely due to mouse events not being fired when pointer outside outline / shadow. Looking into it now.
    - Actually when mouse strays outside the components, component's event filter was hidingControls. Disabled it when moving and seems to be working.

Coming back to snaps now.
- Refactored the snapping code.
- Fixed a bunch of trivial errors.
- Got snap working, but incorrectly.

Decided to rewrite snapping code, as there seems huge scope for improvement.
Cleaned up more than 50% of dense number logic code. Still some way to go.
Turning in for the day. Don't want to throw schedule off.
Atleast, I can start tomorrow with some gumption.

-----
<br>

### November 2:

- Cleaned up the snap code.
- Updated the logic for the updated canvas conventions.
- Tested the snapping logic.
- Rewrote the code for drawing snapping cues.
- Tested and tuned the cues to be clear and symmetrical.
- Further optimised snap point computation code.



