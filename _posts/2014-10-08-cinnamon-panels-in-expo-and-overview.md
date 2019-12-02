---
layout: post
category: how-to 
title: "Cinnamon panels in Expo and Overview"
tagline: "Where is that start menu?"
tags : [mint, cinnamon, tutorial]
---
{% include JB/setup %}

One of the things that I've liked in GNOME 3 is ability to manage workspaces, windows and run application from the overview mode, all beginning from one single gesture. So I'd like to my Cinnamon desktop behave somethat alike.

<!-- more -->

<img src="{{ site.url }}/assets/images/cinnamon-panels-in-expo-and-overview_01.jpg" alt="Cinnamon expo mode with top panel" class="img-fluid" />

## Problem

Simpliest way to run applications in the Cinnamon is to use favorites and menu applets. But they are on the panel, and by default Cinnamon hides panels then entering expo and overview modes - so from expo you can manage only workspaces and windows, from overview - only windows,  and can't run an application (except from Alt+F2 command line) from both of modes.

## Solution

Luckily for us, most Cinnamon UI logic is defined by JavaScript files in the `/usr/share/cinnamon/js/ui/` directory. As you can guess, expo logic is in `expo.js` and overview is in `overview.js`. So what's next?

1\. Open script with superuser privileges in the text editor:

For expo:

{% highlight bash %}
gksu gedit /usr/share/cinnamon/js/ui/expo.js
{% endhighlight %}

For overview:

{% highlight bash %}
gksu gedit /usr/share/cinnamon/js/ui/overview.js
{% endhighlight %}

2\. Find these two lines (marked as 1 and 2):

For expo:

{% highlight javascript %}
...
if (!options || !options.toScale ) {
	Main.enablePanels(); /* 1 */
	activeWorkspace.overviewModeOff(true, true);
}
...
this._gradient.show();
Main.disablePanels(); /* 2 */
{% endhighlight %}

For overview:

{% highlight javascript %}
...
this.workspacesView = new WorkspacesView.WorkspacesView();
global.overlay_group.add_actor(this.workspacesView.actor);
Main.disablePanels(); /* 1 */
...
this.animationInProgress = true;
this._hideInProgress = true;
Main.enablePanels(); /* 2 */
{% endhighlight %}

3\. Comment out these lines and save the file:

For expo:

{% highlight javascript %}
...
if (!options || !options.toScale ) {
// Main.enablePanels(); /* 1 */
activeWorkspace.overviewModeOff(true, true);
}
...
this._gradient.show();
// Main.disablePanels(); /* 2 */
{% endhighlight %}

For overview:

{% highlight javascript %}
...
this.workspacesView = new WorkspacesView.WorkspacesView();
global.overlay_group.add_actor(this.workspacesView.actor);
// Main.disablePanels(); /* 1 */	
...
this.animationInProgress = true;
this._hideInProgress = true;
// Main.enablePanels(); /* 2 */
{% endhighlight %}

4\. Now you need to restart Cinnamon. For this you can use entry in the *Troubleshooting* menu, or command line:

{% highlight bash %}
killall cinnamon && cinnamon
{% endhighlight %}

5\. In some cases expo and overview boxes could be partially overlapped with panels - it's probably your case if you using top panel. 
For both expo and overview, you need to change second parameter value of `set_position` function (Y offset).

For expo, edit `expo.js` again:

{% highlight javascript %}
this._expo.actor.set_position(0, 0); /* change last 0 to the desired value */
this._expo.actor.set_size((primary.width - buttonWidth), primary.height);
{% endhighlight %}

For overview, edit `workspacesView.js`:

{% highlight javascript %}
else {
	workspace.actor.set_position(x, 0); /* change 0 to the desired value */
	if (w == 0)
		this._updateVisibility();
}
{% endhighlight %}

Offset value is related to the panel height, but you need to experiment with this to get desired result, as current Cinnamon theme 
could greatly infuence it. In my case (*New Minty* theme), panel height is about 26, but value of 16 in the `expo.js` and 32 in `workspacesView.js` is fine.

---

<img src="{{ site.url }}/assets/images/cinnamon-panels-in-expo-and-overview_02.jpg" alt="Cinnamon overview (scale) mode with top panel" class="img-fluid" />

## Acknowledgements

This post mainly based on the solution, provided [here](https://github.com/linuxmint/Cinnamon/issues/3001) by [@nfat](https://github.com/nfat).

