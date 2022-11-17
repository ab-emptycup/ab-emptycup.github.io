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

That done, decided to get started with enabling the partition split button.

- Added a UI control for all cupboard sections and positioned it next to the gear.
- Tried a few icons, but not happy with them. Leaving a placeholder icon for now.
- Ran into an issue of on:click not getting triggered.


----
<br>

### November 3:

- Fixed the issue with on:click on getting triggered.
- Tried a few more icons. Rotating the button on changing orientation. Still not 100% satisfied.
- Handled hiding the button on mouseOut()
- Implemented onSplitToggle for the renderer.
- Successfully toggle split orientation. Noticed issue with horizontal split rendering.
- Fixed horizonal split rendering.
- Added fix to remember last used split orientation.

Partition split toggle working as expected now.

Started work on implementing component scale.

----
<br>

### November 5:

Continuing work on implementing scale

- Got the Scale controls to render properly.
- Implemented the component controller.

----
<br>


### November 6:

- Implemented outline rendering on starting scale.
- Fixed outline scaling on moving control.
- Component size now gets updated on finishing scale operation.
- Disabled partition split on scaling or moving.
- Got snap working after a lot of fight.

Still some anamolies in scale UI behaviour.

----
<br>


### November 7:

- Unable to reproduce anamolous UI scale behaviour.
    - Partition split not getting disabled properly on scaling
    - UI controls not being properly enabled on mouseOver

- Noticed issue with scaling partitioned boxes. That needs to be disabled.
    - Ideally, mouse pointer should show an invalid subtext icon on hover
    - Implemented. Cursor changes based on component.isScalable().

- Noticed that snap cues are not rendering for scaling snaps.
    - Fixed an issue with snap cue positioning.
    - Noticing this strange behaviour again where suddenly the UI controls stop showing without any errors.

----
<br>

### November 8:

Unable to get a solid chunk of time to continue work on this thread.

- Fixed more issues with snap cue positioning. Now working properly.
- Noticed a pattern for the wierd UI issue. Having a console log in .svelte resets the wierd. May be an issue with Vite cache?

That's about it for the move functionality. I'll work on things outside the canvas for a while.

- Fixed default selection for the SideSwitch
- Positioned the SideSwitch appropriately.

----
<br>


### November 9:

I keep running into the weird issues with the UI controls. I'll dig into those today.
Before doing that I need to reset my expectations to depress.

A few anamolies that I noticed so far:
    - Wierd positioning of UI controls: move, settings, split
    - Suddenly controls stop showing on refresh
    - Partition split suddenly appears during scaling despite being explicitly blocked.

Right now I'm able to see the wierd positioning. I'll debug that first:

* This may be due to the setting the _container_ div position: to _relative_. I'll test that first.
* Yup. That was it. But, this breaks the SideSwitch positioning. I need to understand this CSS positioning better to resolve this with confidence.
* Issue got fixed by changing the _position_ of all control elements to _fixed_. I'm not sure if that is the correct solution. I could dig into the _position_ property further to understand it's semantics. But, I want to move on.

Not able to reproduce the other two issues again. I have to keep a tab and jump on them when I see them next time.

- Added ModularSidebar with Add, Edit & Decor tabs. Tabs functional.
- Added component accordion. Populated with options.
- __Ran into this strange issue of API container not responding to requests__. I have seen this before. It usually starts working on its own after some time. These little quirks are not good for the dev environment. Just waiting for now...
- Turned out that it was a silent broadband issue.
- Rethinking the organisation of the component list.


-----
<br>

### November 10:

Where should decor options be shown for woodwork? Separate tab? Modal over Modal? Replace grid?

After a lot of consideration, I have decided to prototype the option of replacing grid.
Decor category will be shown in the Add Panel and categories within decor will be shown in
the accordion dropdown for "Decor". Subcategories will be shown in a ribbon on the top of the panel.
Showing options for changing repository and changing catalogue are a question mark.

Having designed a prototype in Figma, I'm satisfied with dumping the decor tab in favor of replacing grid.

I started implementing addComponent functionality. Testing adding a ledge.
Ran into an issue with rendering. Ledge dimensions are NaN.


----
<br>

### November 11:

That was an issue with setting the default dimensions on component addition.
Working on figuring out a clean way of implementing default component sizes.

This rabbit hole goes deep:
- The default sizes for components are being set in the UI.
- UI component doesn't have access & shouldn't be directly accessing woodwork side properties / setting component sizes.
- Ideally, the default sizes need to be set in the component classes.
- Actually, they're being set both in UI and in woodworkjs. Some components don't have their own classes. That may be why.
- Implemented cleaner default starting params for components. Tested some components & fixed issues.


----
<br>

### November 12:


- Fixed issue with UI controls rendering on deleting components.
- Refactored and optimised code for setting defaults.
- Tested all the components and fixed a lot of issues.
- Refactored LoftRenderer & WardrobeRenderer out.


----
<br>

### November 14:

Trying to fix the issue of Kalash not showing up. Seems to be related to some images not being set properly.
Ran into another issue of OTG not rendering properly.

I've been stuck on this for too long. May be its better to come back to this later. I'll give it another 30min at max.
I'll atleast try to fix the Kalash issue. It seems the image encoding is broken? Gave up that efforts. The image is fine. But there is some issue with _loadScaledImage()_ function that is loading image with improper scale. Don't feel like fixing that now. I have already spent more than a couple of hours on this.

Implemented a switch for _modular-container_ when decor is selected in the AddPanel.
Got the switch working correctly. But every switch was triggering an entire canvas reload.
So, fixed the switch to just apply _display: none_ class on the container div appropriately. Still testing.


----
<br>

### November: 15

Neglected to log :(


----
<br>

### November 16:

- Added a temporary fix to disable scroll for DecorGallery beyond viewport height by hardcoding.
- Implemented toggle buttons for subcategory selection.
- Converted decor options into toggle for gallery and removed close button & rearranged gallery ribbon.
- Reorganised the decor options into "Appliances", "Prayer", "Wardrobe" etc.
- Fetching and filtering the actual furnishing catalogue in Decor gallery.
- Showing properly shaped thumbnail previews for furnishings now.


----
<br>

### November 17:

- Added 'type' & 'category' fields to decor option format to work seemlessly with the furnishing catalogue.
- Connected FurnishingRenderer to handle component add.
- Added 'furnishings' to woodwork_options & 'frontview_ref' for each furnishing.
- Closing DecorGallery and updating UI state on adding component.
- Fixed inconsistency in dimension unit conventions for furnishings (inches / mm / px).
- Setup sane default position on component add.
- Adding furnishings successfully now. But, the issue with texture / pattern rendering on canvasObject still persists.

