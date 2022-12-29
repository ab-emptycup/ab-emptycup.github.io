---
layout: page
title: December Regroup
---


This is a log of regroup efforts during the last week of December after a 2 week off due to personal commitments.

Things to do:

- Refactor and test Wardrobe, TVSet sections.
- Add export links for woodworks.
- Review all issues on Github Project.
- Prepare TODO for v2 release.

### December 26:

First assessing the environment and resetting.

- Fixed issue _azure-identity_ python package not being installed.
- Cleared a long pending issue with an ugly _requirements-py3.txt_.
- Verified that the Woodwork Save issue not occuring now. Not sure what caused/fixed it.
- Noticed an issue with scaling boxes with partitions using the dimension editor.
- Noticed that box snapping off by an inch when snapping to corners (boxes on the other side).
- Fixed issue with scaling boxes with partitions when using the dimension editor.
- Fixed issue with improper box snapping at corners.
- Fixed issue with front view rendering for furnishings in modular view.


----
<br>

### December 27:

- Fixed issue with Wardrobe not being saved due to 500 from API (box depth wasn't being properly intialized).
- Ran into a strange issue with _api_ object not initializing on the frontend. Wasted some time testing a bunch of things. Finally, the issue got fixed automatically, by creating a new branch and testing there. Still not clear what caused it or how it got fixed.
- Noticed an issue with dressing section rendering. It was rendering white. Fixed it now.
- Noticed an issue with external drawer rendering also. It was erroring out on render. Fixed it now.



----
<br>

### December 28:

Evaluating must fix issues before release:

- Not able to select overlapping room
- Click and scale not working for rooms
- 8" discrepancy with floors
- Main entrance door
- Balcony scaling
- Floorplan 3D preview taking a lot of time.
- Railing: Glass, Steel, Concrete
- Save button gets stuck in loading
- Spacing above "No woodworks. Add in 2D."
- Reduce margin for woodwork map
- Delete woodwork partitions
- Automatically add hotspot near entrance.
- Import furnishings
- Fix dressing section composition.


This is what I found till drafting floorplan. Apart from this, there's more on the backend:

- Refactor _AssetStore_
- Remove _ref_ columns from DB.
- Remove theme related code from the backend.
- Add "TimeTaken" as a render table column.
- Setup _emptycup3d.azuredge.net_


----
<br>

### December 29:

Today, I'm going to start with getting the composition for the Dressing section to work.
Then, I will get internal sections working using a box level UI control.

- Got dressing section composition working properly. Turned out to be not so complicated as I had feared.
- Implemented the door toggle UI control. Functionality not yet implemented.