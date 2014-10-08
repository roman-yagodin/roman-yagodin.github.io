---
layout: post
category: how-to 
tagline: "Supporting tagline"
tags : [mint, cinnamon, tutorial]
---
{% include JB/setup %}

# Show Cinnamon panels in the overview

## Problem

One of the things that I've liked in GNOME 3 is ability to manage workspaces, windows and run application from overview, beginning from one single gesture. So I'd like to my Cinnamon desktop behave somethat same.

Simpliest way to run applications in the Cinnamon is to use favorites and menu applets. But they are placed on the panel, and by default Cinnamon hides panels then entering overview (and expo) modes - so from overview you can manage only workspaces and windows, and can't run an application (except from Alt+F2 command line).

## Solution

Luckily for us, most Cinnamon UI logic is defined by JavaScript files in the `/usr/share/cinnamon/js/ui/` directory. As you can guess, overview logic is in `overview.js`. So what's next?

1. Open `overview.js` with superuser privileges in the text editor:

  ```shell
  gksu gedit /usr/share/cinnamon/js/ui/overview.js
  ```

2. Find these two lines (marked as 1 and 2):

  ```javascript
  ...
  this.workspacesView = new WorkspacesView.WorkspacesView();
  global.overlay_group.add_actor(this.workspacesView.actor);
  Main.disablePanels(); /* 1 */
  ...
  this.animationInProgress = true;
  this._hideInProgress = true;
  Main.enablePanels(); /* 2 */
  ```

3. Comment out these lines and save the file:

  ```javascript
  ...
  this.workspacesView = new WorkspacesView.WorkspacesView();
  global.overlay_group.add_actor(this.workspacesView.actor);
  // Main.disablePanels(); /* 1 */
  ...
  this.animationInProgress = true;
  this._hideInProgress = true;
  // Main.enablePanels(); /* 2 */
  ```
  
