---
layout: post
category: how-to
title: "GTK decoration layout"
tagline: "Customize GTK 3 client-side decorated windows"
tags : [gtk, cinnamon]
---
{% include JB/setup %}

Many great GNOME 3 applications are used widely across various desktop environments. Most of them use GTK+ client-side decorations (csd) instead of window manager borders, which makes them look as strangers outside GNOME Shell. In this post I want to show you how to tweak window buttons layout for csd-enabled applications.

<!-- more -->

<img src="{{ site.url }}/assets/images/gtk-decoration-layout_01.png" alt="Classic window manager decorated window (Nemo) along with client-side decorated window (Nautilus)" class="img-fluid" />

<p style="text-align:center">Classic window manager decorated window (Nemo) along with client-side decorated window (Nautilus).</p>

## Facts

Since GTK+ 3.10, GtkHeaderBar widgets use `gtk-decoration-layout` setting value
to display window control buttons in the right place & order. Default value is
`menu:maximize,minimize,close` (format is the same as for window manager buttons layout).

## Solution for Cinnamon

*Cinnamon* provide a way to override default `gtk-decoration-layout` setting value via `dconf` key `gtk-decoration-layout` in the  `org.cinnamon.desktop.interface` section.

Let's set close button + menu to the left, and minimize button to the right. You could use `dconf-editor` to change setting value from GUI. From command-line, it should be like this:

{% highlight bash %}
gsettings set org.cinnamon.desktop.interface gtk-decoration-layout 'close,menu:minimize'
{% endhighlight %}

Note what some buttons names are not supported, these are: **above**, **stick**, **shade** and **separator**. Hopefully, this will change in the future GTK+ versions.

## More common way

For desktop environments, which don't override `gtk-decoration-layout` setting, just change (or define) it in `~/.config/gtk-3.0/setting.ini` like this:

{% highlight ini %}
[Settings]
gtk-theme-name=Adwaita
...
gtk-decoration-layout=close,menu:minimize
{% endhighlight %}

Session restart would be needed to apply changes. Also, if there are no `settings.ini` file, just create new one and add `[Settings]` line.

## Results

<img src="{{ site.url }}/assets/images/gtk-decoration-layout_02.png" alt="Classic window manager decorated window (Nemo) along with client-side decorated window (Nautilus) - after changes" class="img-fluid" />

<p style="text-align:center">Classic window manager decorated window (Nemo) along with client-side decorated window (Nautilus) - after changes.</p>

## Useful links

- [Client-side decoration, continued](https://blogs.gnome.org/mclasen/2014/01/13/client-side-decorations-continued/)
- [GTK3 documentation about gtk-decoration-layout setting](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-decoration-layout)
- [Muffin Window Buttons Layout]({{ BASE_PATH }}/how-to/2014/10/22/muffin-window-buttons-layout/)
