---
layout: post
category: how-to
tagline: "Supporting tagline"
tags : [cinnamon, muffin]
---
{% include JB/setup %}

One of great things about Linux desktops is ability to customize window title buttons layout - according to your taste or regular job specifics. If you are using *Cinnamon*, this instruction is for you - but majority of things are same for *GNOME 3*, *GNOME Flashback*, *Cinnamon* and *MATE* - as they are using similar window managers, derived from *metacity* - default window manager in *GNOME 2*.

<!-- more -->

---

<img src="{{ site.url }}/assets/images/muffin-window-buttons-layout_01.png" alt="Editing muffin buttons layout in dconf-editor" class="img-responsive" />

## Desktop environments and window managers

Here are the desktops and default window managers:

| DE 				| Default WM                    |
|-------------------|-------------------------------|
| GNOME 2 			| metacity						|
| MATE 				| marco (metacity fork)			|
| GNOME 3 			| mutter = metacity + clutter	|
| GNOME 3 Flashback	| mutter						|
| Cinnamon 			| muffin (mutter fork)			|

## Setting up

Buttons layout and some other WM options are stored in the *dconf* keys. For *Cinnamon's muffin*, we should
change value of the key `org.cinnamon.desktop.wm.preferences.button-layout` or the key `org.cinnamon.muffin.button-layout`
to override value of the first key.

Some other desktops:

- `org.gnome.shell.overrides.button-layout` - for *GNOME 3*
- `org.gnome.desktop.wm.preferences.button-layout` - said to work in *GNOME Flashback / Classic*

Here are list of button names:

- **stick** - toggle "show on all workspaces"
- **above** - toggle "always on top"
- **menu** - window menu
- **shade** - toggle "roll / minimize to header"
- **spacer** - space between buttons
- **close, maximize, minimize*** - as they sounds

Note what standard *Cinnamon* window settings do not have ability to add some buttons, like **above**, <del>**shade**</del> (present since 2.4) and also **spacer** -
so we should use `dconf-editor` for GUI or `gsettings set` command in the terminal to get things done.

<img src="{{ site.url }}/assets/images/muffin-window-buttons-layout_04.png" alt="Editing muffin buttons layout in Cinnamon windows settings" class="img-responsive" />

## Examples

Value of `button-layout` key is a comma-separated list of button names, like `close:shade,minimize`. Colon (:) is used to distinguish left and right side.

Format of `gsettings` command:

{% highlight bash %}
gsettings set <key> button-layout <value>
{% endhighlight %}

Move all 3 default buttons to the left:

{% highlight bash %}
gsettings set org.cinnamon.muffin button-layout 'close,maximize,minimize:'
{% endhighlight %}

![3 default buttons]({{ site.url }}/assets/images/muffin-window-buttons-layout_02.png)

My current layout:

{% highlight bash %}
gsettings set org.cinnamon.muffin button-layout 'close,above:shade,minimize'
{% endhighlight %}

![My current buttons layout]({{ site.url }}/assets/images/muffin-window-buttons-layout_03.png)

## Theme issues

- Some buttons could miss icons - it's very common issue. By example, *Adwaita* theme have no icon for **above** button.

- I also encounter problem with **spacer** button in both *Cinnamon 2.0* and *GNOME 3.8* with *Adwaita* theme - space is visible only if window is shaded (minimized to header). In normal state, spacer is not visible.

## Feedback

Let me know, if I've messed up with something! I would also want to know
about which button layouts you are using and what theme or WM issues you have encountered.
