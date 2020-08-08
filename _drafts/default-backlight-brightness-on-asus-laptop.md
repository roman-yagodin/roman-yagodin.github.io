---
layout: post
title: "Set default backlight brigthness on ASUS laptop"
tagline: "Customize client-side decorated windows"
category: how-to
tags : [linux, backlight, brigthness]
---
{% include JB/setup %}

During my last years with Linux, laptop power management in general and backlight control in particular is one of the most annoying things. I came through many weirdnesses like not working brightness buttons, controls or applets - but with my current [LMDE 2 Betsy]() these issues are long forgotten. Except one thing - after boot backlight brightness always set to minimum. So I have to adjust brightness manually after every boot and also desktop manager screen is too dim to be looking good.

<!-- more -->

<img src="{{ site.url }}/assets/images/gtk-decoration-layout_01.png" alt="Classic window manager decorated window (Nemo) along with client-side decorated window (Nautilus)" class="img-responsive" />

In this post I want to share my recent experience with solving backlight brightness issue on my ASUS K55N laptop.

My current system:

{% highlight bash %}
$ uname -a
Linux xyz 3.16.0-4-amd64 #1 SMP Debian 3.16.7-ckt20-1+deb8u1 (2015-12-14) x86_64 GNU/Linux
{% endhighlight %}

Historically, my first solution was to add `xbacklight` utility to autostart:

{% highlight bash %}
xbacklight -set 100 # first variant
{% endhighlight %}

The second one was using `xdotool` to simulate pressing on brightness buttons after logging in - somewhat ugly, I know:

{% highlight bash %}
xdotool key --repeat 25 XF86MonBrightnessUp # second variant
{% endhighlight %}

As both solutions not working anymore, I start to seek more general one, and after some time found that there is ...

...

> **Note:** The `acpi_video0` is variable part - in your system it could be `intel_backlight` or something different - just check `ls /sys/class/backlight` output.

I've added the code show below to `/etc/rc.local` to execute on boot for every user. Note that it will be executed with superuser rights (no `sudo` required) and desktop manager session is affected also.

{% highlight bash %}
# set backlight brightness to max
cat /sys/class/backlight/acpi_video0/max_brightness > /sys/class/backlight/acpi_video0/brightness
...
exit 0 # don't delete me!
{% endhighlight %}

One more thing: I'd like the backlight set to maximum only if my laptop is connected to the AC power supply. I think it's OK to have minimum (default) backlight brightness when booting without one, as it save some battery time.

So, let's check another [ABI](https://www.kernel.org/doc/Documentation/ABI/README) entry:

{% highlight bash %}
# check the power supply is connected
if [ 1 -eq $(cat /sys/class/power_supply/AC0/online) ];
then
	# set backlight brightness to max
	cat /sys/class/backlight/acpi_video0/max_brightness > /sys/class/backlight/acpi_video0/brightness
fi
{% endhighlight %}

## Links

I hope the described solution would be useful to you, but generally it shouldn't. Here are some links I've found enlightening:

* [https://wiki.archlinux.org/index.php/Backlight](https://wiki.archlinux.org/index.php/Backlight)
* [https://www.kernel.org/doc/Documentation/ABI/stable/sysfs-class-backlight](https://www.kernel.org/doc/Documentation/ABI/stable/sysfs-class-backlight)
