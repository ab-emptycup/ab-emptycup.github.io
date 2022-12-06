---
layout: page
title: Improving modular.js
---

This is a continuation of last month's efforts on [rewriting modularjs](/devlog/rewriting-modularjs).
<br>


### December 5:

Things to do:

1. Implement Dimension Editor for components.
2. Handle special case where component too small for UI controls.
3. Render blocking components and sides in frontview.
4. Refactor out 'freezeExternal'

Started working on Dimension Editor.

- Added UI control for toggling the editor.
- Styled the control to stay toggled on click.
- Got EditPanel and the EditControl to stay in sync.
- Added edit inputs to the EditPanel
- Got unit conversion working on the panel
- Got the edit inputs to update the component with undo.


-----
<br>

## December 6:

- Got the UI control to adjust position while the component is being updated.
- Cleaned up the code and fixed a couple of corner cases.
- Got scale controls to switch off if the component is too small.
- Got side corners to render in front view of adjacent sides.
- Fixed an issue with DecorGallery not toggling off from the AddPanel.


