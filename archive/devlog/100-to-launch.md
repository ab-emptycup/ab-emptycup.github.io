---
layout: page
title: 100 hours to launch
---


This sprint was abandoned midway due to a sharp change in execution strategy.


-----


This is a 100 hour countdown to launch of [emptycup3d.com]().



### Hour 1:

I just refactored _Scene.js_ from _libscenejs_. Todo next:

- Debug and fix issues with refactored code
- Clean up and commit.
- Evaluate if the current model loading process is blocking.
- Start refactoring the _WalkinLoader.js_

Finished debugging. Works apart for model loading.

---
<br>

### Hour 2:

Next steps are:

- Remove the old _Walkin.js_ and commit.
- Clean up the _WalkinLoader.js_.

Done:

- Finished cleaning up the code. Committed.
- Reorganised the loaders into scenejs/loaders. Committed.
- Started rewriting / refactoring _WalkinLoader.js_ and it is, UGLY.


---
<br>

### Hour 3:

Cleaned up the overall flow of _WalkinLoader.js_. This is going to be a lot cleaner once the refactor is done.
I still need to refactor / rewrite the parsing and the loading code.

---
<br>

### Hour 4, 5:

Still working through _parseMaterial()_


---
<br>

### Hour 6, 7, 8:

- Spent some time reviewing a PR that has been pending for almost a month now.
- Followed up on internship post blast with Amrita. Scheduled a call at 4pm.
- Created a form for students to apply without submitting PR.


---
<br>

### Hour 9, 10:

Refactored texture and lightmap loading flow. Dropped call backs in favour of async.
I still need to untangle the whole caching mechanism for images.


---
<br>

### Hour 11:

Had call with Amrita faculty regarding the transparency of the application process.
Discussed the internship situation at KLU as well with Bharat.


---
<br>

### Hour 12:

It is still just wading through the refactor. I have to get out of this swamp by the end of the day.
Identified and resolved a bunch of issues debugging the page load.


---
<br>

### Hour 13:

Had a long meeting with the RBL bank executive for current account opening. This is a blocker
for the product launch as the payment gateway integration needs these formalities to complete.


---
<br>

### Hour 14:

Had a productive call with the Amrita faculty regarding the issue with internships.
Expecting 11month interns to be available by mid August.


---
<br>

### Hour 15, 16, 17, 18:

Fixed all the issues in debugging and finally got to a place where the model was loading smoothly
though the textures are still not loading. Apart from that the original meaningless error that
triggered the whole refactor seems to popped up again.

On digging further, I realised that this meaningless error was being thrown by a piece of
dumb caching code that was failing because of the furnishing model json served by ABS being empty.
So, it turns out this had nothing to do with _scenejs_ at all.

Time to turn in for the day hoping for sweet dreams of stabbing some unknow authors of caching code
repeatedly in the neck with a long rusted ice-pick.


