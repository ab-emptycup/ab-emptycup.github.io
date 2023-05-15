---
layout: page
title: February Week 4
---

May 14 - May 20<br>
Week #: 20/52<br>


### Monday: May 15


- Setting up the dev environment after almost 1.5 months: Docker deployment up.
- Layout page loading successfully, although there are some wierd "chunk" errors.
- 3D page loading successfully, but furniture not loading.

On checking the code, it seems I left the codebase in the middle of a debugging session.
Checking the debug logs shows that the furnishing component's model json file is "Zero Bytes".
It seems my furnishing copy script failed copying.

The next step for me is to reset the furnishing catalogue's model json's. Not sure, what the state
of the `recat` scripts are. I need to clean those up. Take a status report on all the furnishings
from the _emptycup3d_ catalogue.

