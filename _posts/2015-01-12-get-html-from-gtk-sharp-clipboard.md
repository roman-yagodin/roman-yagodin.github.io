---
layout: post
category: how-to
title: "Get HTML from GTK# clipboard"
tagline: ""
tags : [gtk-sharp, clipboard, mono]
---
{% include JB/setup %}

Developing a cross-platform application would never be easy job, but I consider GTK# framework as one of the solid options to provide cross-platform UI, though the lack of documentation is embarassing sometimes. In this post I want to show an example of using `Gtk.Clipboard` object to get HTML markup from the clipboard.

<!-- more -->

<img src="{{ site.url }}/assets/images/get-html-from-gtk-sharp-clipboard_01.png" alt="Paste table from LibreOffice Writer to GTK# application as HTML" class="img-responsive" />

## Problem

GTK# documentation and examples do not provide excessive information about using `Gtk.Clipboard` object to get various types of content. To get text from clipboard, the `Gtk.Clipboard.WaitForText()` method could be used, but how to get, by example, HTML table from LibreOffice Writer document or formatted text from webpage?

## Solution

In this solution we: 

1. Create target using `Gdk.Atom.Intern()` method, passing MIME type string `text/html` to it. 
2. Get selection object by using `Gtk.Clipboard.WaitForContents()` method for created target.
3. If the selection is not null, then it's `Data` property generally contains UTF-8 encoded string with HTML markup.

{% highlight C# %}
// create clipboard object
var clipboard = Gtk.Clipboard.Get (Gdk.Atom.Intern ("CLIPBOARD", true));

// create target using MIME type
var target = Gdk.Atom.Intern ("text/html", true);

// trying to get HTML markup
var selection = clipboard.WaitForContents (target);

if (selection != null)
{
	// data is UTF-8 encoded string
	textview1.Buffer.Text = System.Text.Encoding.UTF8.GetString (selection.Data, 0, selection.Data.Length);
}
else
{
	textview1.Buffer.Text = "No selection";
}
{% endhighlight %}

The solution is currently tested only on Linux with Mono 3.10. 

Note, that `Gtk.Clipboard.WaitForTargets()` method in the GTK# 2.12 seems to have broken interface. It defined as `bool WaitForTargets (Gdk.Atom targets, out int n_targets)`, but should be something like `bool WaitForTargets (Gdk.Atom [] targets, out int n_targets)` to return array of available targets. As a result, we can't see what targets are available in the clipboard, but only a number of them:

{% highlight C# %}
// create clipboard object
var clipboard = Gtk.Clipboard.Get (Gdk.Atom.Intern ("CLIPBOARD", true));

// create dummy target
var target = new Gdk.Atom (IntPtr.Zero);

int n_targets;
if (clipboard.WaitForTargets (target, out n_targets))
{
	// for me, returns about 12 or 13 targets
	textview1.Buffer.Text = n_targets.ToString (); 
}
{% endhighlight %}

## More to Explore

We got the basic example to work, but many things are need to be explored: 

* Primary: the selection data encoding seems to not always UTF-8, so we need a way to determine the encoding. 
* Which other common MIME types are supported by `Gtk.Clipboard`? 
* How this code will behave on the different platforms?

