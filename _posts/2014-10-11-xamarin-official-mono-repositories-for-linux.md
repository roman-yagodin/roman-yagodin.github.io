---
layout: post
category: how-to 
title: "Xamarin official Mono repositories for Linux"
tagline: ""
tags : [mono, linux, debian, xamarin]
---
{% include JB/setup %}

**Great news for all Mono developers on Linux!** Recently *Xamarin* introduced [official Mono repositories for Linux](http://www.mono-project.com/download/#download-lin) (Debian, Ubuntu, RedHat, SUSE and derivatives). Currently it contains Mono 3.10.0 and MonoDevelop 5.5.0 - a major improvement at least for Debian users (currently Mono 3.2.8, MonoDevelop 4.0.12 even in Sid).

<!-- more -->

<img src="{{ site.url }}/assets/images/xamarin-official-mono-repositories-for-linux_01.png" alt="Xamarin Mono downloads page" class="img-fluid" />

## Installation in Debian

Add repository line to your `sources.list` and install Xamarin [GPG key](http://download.mono-project.com/repo/xamarin.gpg). The most simple way to do that is using *software-properties-gtk* or *mintsources* (in case you are using Mint or LMDE). It also can be done from command line:

{% highlight bash %}
sudo -i
echo "deb http://download.mono-project.com/repo/debian wheezy main" > /etc/apt/sources.list.d/mono-xamarin.list
wget http://download.mono-project.com/repo/xamarin.gpg
apt-key add - < xamarin.gpg
{% endhighlight %}

Now we have to update apt cache and upgrade packages:

{% highlight bash %}
sudo apt-get update
sudo apt-get upgrade
{% endhighlight %}

Now get some tea (coffee) and sandwiches and wait... In case of problems check [official installation guide](http://www.mono-project.com/docs/getting-started/install/linux/).

---

<img src="{{ site.url }}/assets/images/xamarin-official-mono-repositories-for-linux_02.jpg" alt="MonoDevelop IDE 5.5 with GTK# designer and Mono 3.10" class="img-fluid" />

