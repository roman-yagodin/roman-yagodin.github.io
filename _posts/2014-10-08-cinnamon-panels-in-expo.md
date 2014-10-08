---
layout: post
category: how-to 
tagline: "Supporting tagline"
tags : [mint, cinnamon, tutorial]
---
{% include JB/setup %}

# Show Cinnamon panels in the overview

## Problem

One of the things that I've liked in GNOME 3 is ability to manage workspaces, windows and run application from expo, beginning from one single gesture. So I'd like to my Cinnamon desktop behave somethat same.

Simpliest way to run applications in the Cinnamon is to use favorites and menu applets. But they are placed on the panel, and by default Cinnamon hides panels then entering expo (and overview) modes - so from expo you can manage only workspaces and windows, and can't run an application (except from Alt+F2 command line).

## Solution

Luckily for us, most Cinnamon UI logic is defined by JavaScript files in the `/usr/share/cinnamon/js/ui/` directory. As you can guess, expo logic is in `expo.js` and overview in `overview.js`. So what's next?

1. Open script with superuser privileges in the text editor:

		{% highlight bash %}
		gksu gedit /usr/share/cinnamon/js/ui/expo.js
		{% endhighlight %}

	for overview:

		{% highlight bash %}
		gksu gedit /usr/share/cinnamon/js/ui/overview.js
		{% endhighlight %}

2. Find these two lines (marked as 1 and 2):

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

	Variant for overview:

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

3. Comment out these lines and save the file:

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

	Variant for overview:

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

4. For those who'd prefer panel on top, more tweaks needed as expo / overview boxes could be partially overlapped with panel.

	For expo, edit `expoThumbnail.js`:

	*Old solution not working* :(  
	
	For overview, edit `workspacesView.js`:

		{% highlight javascript %}
		else {
			workspace.actor.set_position(x, 0); /* change 0 to panel height */
			if (w == 0)
				this._updateVisibility();
		}
		{% endhighlight %}

5. Now you need restart Cinnamon. For this you can use entry in the Troubleshooting menu, or use command line:

		{% highlight bash %}
		killall cinnamon && cinnamon
		{% endhighlight %}
  
## Thanks

Thanks [nfat](https://github.com/nfat) for the ideas described [here](https://github.com/linuxmint/Cinnamon/issues/3001).
