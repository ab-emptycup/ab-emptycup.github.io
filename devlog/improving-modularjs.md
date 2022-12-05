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

