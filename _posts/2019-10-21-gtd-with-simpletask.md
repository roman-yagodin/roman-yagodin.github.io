---
layout: post
category: guide
title: "GTD with Simpletask"
tagline: "a TL;DR guide"
tags : [GTD, trusted system]
---
{% include JB/setup %}

This is a TL;DR guide of *Getting Things Done (GTD)* implementation using [Simpletask][] app by [Mark Janssen][] as a core component of trusted system, heavily based on [Alex Armstrong's work][] including my thoughts and personal experience about it over past couple of years. The content is restructured to center on GTD-related things. Consider it incomplete and very eccentric.

<!-- more -->

> *Simpletask* uses the [todo.txt][] syntax, but has sufficient differences and quirks of its own to be worth describing in detail -- at least, that's the story I'm going with. I actually began this guide as an exploration of my own trusted system. *Personal workflows are by definition eccentric*; I have included only what seems to me to be broadly useful.
>
> This implementation of GTD covers the "standard" classifications: next actions by context, projects, somedays, agendas by person and meeting, etc. In a departure from strict GTD, each entry in these lists is also tagged with an area of focus, interest or responsibility. I find that the ability to slice the system by this extra dimension is worth the additional complexity at the processing and organizing stages. Limitations, issues and workarounds are discussed at the end.
>
> -- Alex Armstrong, the author of original guide.
 
> Your system has to be easy enough (and complete enough) that you will be motivated to work it even when you have the flu. The system is only as good as what you're willing to maintain when you don't feel like it.
>
> -- David Allen, "[Let the Lists Fall Where They May](http://www.davidco.com/newsletters/archive/0810b.html)"

* * * * *

## Entries

I refer to every line in your `todo.txt` as an "entry" to differentiate them from tasks. Simpletask takes a broader view of what constitutes a `todo.txt` file.
In *this* implementation the `todo.txt` format provides a large chunk of your trusted system.

Entries may belong to one list (`@something`) and they may have one or more tags (`+something`) assigned to them. They may also utilize due dates (`due:2014-04-2`) thresholds (`t:2014-04-3`), recurrance (`rec:1w`) and priorities (`(A)`, ..., `(Z)`).

## Lists (`@`)

Simpletasks collects all `@somethings` in your entries and calls them *lists*.

Lists hold all entries on the first four *Horizons of Focus*: from *Runway* to *30,000 feet*, or *Next Actions* to *Goals & Objectives*.  If you find this format appropriate, you could feasibly include items from the remaining two altitudes: *Vision*, *Purpose* and *Principles*.

**Lists are mutually exclusive!** If an entry can be placed in more than one list, you need to clarify either the entry or your lists.

## Tags (`+`)

Simpletasks collects all `+somethings` in your entries and calls them *tags*.

Tags specify *areas of focus, interest or responsibility*, as well as *agendas for people or meetings*.

## Inbox (Capture/Collect)

The inbox consists of *all entries that have not been assigned to a list*. They are typically not tagged, either. Although I will often revise entries before tagging and assigning them to another list, I generally preserve the original creation date.

**You don't need a list called `@Inbox`!** First of all, it will just slow you down at the collection phase. If you want to view just your *Inbox*, filter by `-` in the left drawer.

## Next Actions / Contexts (Runway)

*Next actions* are filed in lists that begin with an *at-sign* (`@`), one for each context. The *at-sign* is an established shorthand that reinforces the idea that the context (place or tool) is required for the action to be performed. More importantly, the *at-sign* makes these lists sort above the others, so you can find them more quickly.

The examples of GTD contexts are:

```
@@agendas
@@anywhere
@@calls
@@computer / @@laptop
@@errands
@@home
@@office / @@work
```

**Уou may (and must) define your own contexts!** By example, I like to have context `@@buy` - for any optional triffles I'd want to buy during accidental shopping; and also context `@@ingame` - it's just like `@@computer`, but when you use it for fun. 

Next actions are tagged with an area tag and, for entries relating to communication, an agenda tag (either a person or meeting). 

### Agendas

Agendas may be listed under `@@agendas` (for face-to-face and impromptu communications) or required context (e.g. `@@calls`, `@@computer`, etc.) but *not* both.

All tags that begin with a capital letter refer to agendas -- that is, to people or meetings.

Example tags:

```
+Mom
+JSmith
+StaffMeeting
```

Place agenda entries in the appropriate context list and then tag them with an area.

Example entries:

```
Tell +Bob about the party @@agendas +fun
Email +DevTeam re: new client @@online +work
```

People and meetings you refer to often can be added to a hidden entry (see below) for easy access.

## Projects (10,000 ft)

A list called `@Projects` with an entry for **every multi-step outcome you are committed to completing within the next year**. Each project entry is tagged with an area and, if applicable, an agenda.

For code-related project you could think of each milestone as of GTD project.

Examples:

```
Clean out the garage +household @Projects
Release R7.Documents module v1.11 +work @Projects
```

## Someday/Maybe (Incubate Runway/10,000 ft)

A list called `@Someday` with an entry for every project (multi-step outcome) or single action you are incubating -- i.e., that would like to periodically review but are not committed to moving on, yet. Each someday entry is tagged with an area and, if applicable, an agenda, allowing you to view potential commitments along with your current ones.

Example: `Learn to play the piano +creativity @Someday`

You could feasibly have multiple Someday/Maybe lists like `@Someday-Soon` or even `@Someday-Never`, if you need the additional granularity --
or just use Simpletask priorities.

Use the `@Someday-Never` to RIP things that you strongly doesn't want and have strong reasons to not to do, but still need to remember sometimes.

## Tickler (Incubate Runway/10,000 ft)

A list called `@Tickler` contains **all tickled items which are not actions**. Tickled items are all entries with a threshold date; if their threshold has not passed, I like them to also have a priority of `(B)`.

Tickled actions are not included in this list; they are placed under the appropriate context.

## Waiting For (Runway)

A list called `@WaitingFor` with an entry for each delegated action, tagged with both area and agenda.

Example: `+JSmith re: conference +consortium @WaitingFor`

## Areas (20,000 ft)

A list called `@\_Areas` with entries identifying all your areas of focus, interest or responsibility. There is overlap between this horizon and the area tags (described below), but a 1-to-1 correspondence is not obligatory. How you set up this horizon depends on how you think about your life and how it makes sense to carve up your commitments.

Note: the underscore in front of this list is merely to have it sort to the bottom of your lists.

All lowercase tags refer to areas of focus, interest or responsibility. These generally relate to the *20,000 feet horizon*, but will probably be more granular. There's no rule here; you will need as many areas as you need.

A word of warning, however: **avoid making area tags too specific** (so that they basically map to your projects). Most area tags will be somewhere between projects and areas (or approximately *25,000 feet*)

Examples:

```
+gtd
+blog
+health
+household
```

Example entries:

```
Family +family @_Areas
Health, Vitality & Well-Being +health @_Areas
Profession, Self-improvement +profession +gtd @_Areas
Finances +finances @_Areas
Household +household @_Areas
Hobbies +blog +painting +rpg  @_Areas
```

To make sure that these are always available, define them in your `@_Areas` entries or add them to a hidden entry (see below).

## Goals & Objectives (30,000 ft)

A list called `@\_Goals` with an entry for **every outcome you are committed to completing within the next 2-5 years**, tagged with an area and, if applicable, an agenda. Goals are treated basically as long-term projects.

Example: `Attain some promotion +career @\_Goals`

* * * * *

## Other Features

### The Left Drawer

The left drawer allows you to view your system by any combination of horizon, area and agenda. This is a rough sketch of how your left drawer should look:

- Lists
    - Inbox
    - Contexts
    - Higher Altitudes
- Tags
    - Agendas
    - Areas

The most frequently used ways to slice your system -- contexts and areas -- are the quickest to reach, being at at the top and bottom, respectively. Less used stuff -- higher altitudes, agendas -- is in the middle.

You can choose multiple lists and tags to slice your trusted system in various ways. For example, you can see all the `@@calls` you have to make for `+work`, the `@Projects` relating to your `+family` or all the `+fun` things you might do `@Someday`.

### Hidden Entries

These can serve as placeholders to preserve your lists and tags when they do not contain any items.

Examples:

```
h:1 Contexts: @@agendas, @@anywhere, @@calls, @@computer, @@errands, @@home, @@office
h:1 Other Lists: @Projects, @Someday, @Tickler, @WaitingFor, @_Areas, @_Goals
h:1 Contacts: +Mom, +JSmith, etc.
```

Hidden entries can also be used to store some private entries which you wouldn't like to be shown on your phone screen in public accidentally --
while it's possibly better to have separate todo file for that.

### Due Dates

Per GTD, I only use due dates for the "hard landscape", such as appointments, rather than estimations of when I'd like to do something. I also add them to projects to indicate deadlines (after which completion becomes moot).

For time-sensitive actions you could use prefix times like so: `[10:15] Taskname`. Or suffix times so: `due:2019-06-20 T10:15` - this looks almost like an [ISO datetime](https://www.w3.org/TR/NOTE-datetime) (`2019-06-20T10:15`).

That said, I find Simpletask's calendar integration to be really clunky, and I have begun adding items straight to the calendar, which I find problematic.

### Threshold Dates

Threshold dates allow you to incubate actions or reminders (tickled entries). I like to add the `(B)` priority to all newly created tickled entries, while it is not required. Tickled actions are filed under the appropriate context. For reminders, you can use the `@Tickler` list.

The priority is removed when the entry has been "tickled" (the threshold has been passed).

### Recurrence Dates

TBD.

### Priorities

GTD does not (and should not) have a priority system. I use the `todo.txt` priority syntax to help me filter three kinds of entries:

- Entries with `(A)` priority are "hot": they are actions that I plan (not would *like*) to do today or at least tomorrow. I update this list daily.
- Entries with `(B)` priority are "tickled": all actions or reminders with a threshold date have this priority until the threshold is passed.
- Entries with `(D)` priority are just GTD hints I like to leave above other entries in the list, something like that:

```
(D) Check context lists
(D) Plan to complete within the next year @Projects
```

This leaves `(C)` priority reserved for future use, as only `(A)`, `(B)`, `(C)` and `(D)` priorities are useful (have a color) in the current Simpletask version.

**Projects and higher altitudes never have priorities.**

## Saved Filters (The Right Drawer)

Saved filters allow you to bring up or review aspects of your GTD system. The ones I've found most useful are:

### Hotlist

The *Hotlist* shows me anything with a priority. In this way I see all my "hot" actions for today or tomorrow, as well as all "tickled" entries (incubated actions with a threshold that have become relevant).

The hotlist is not a GTD concept, but in interviews *David Allen* has accepted the it as a potentially useful, as long as it does not become a system unto itself. It also allows an incubation system with date-specific triggers.

### Common

- Hide completed tasks and tasks with threshold date in future.

### Review

- Show all tasks (including complete and tasks with threshold in the future).
- Sort with Completed on top - to avoid scrolling:

Base state:

```
x Completed entry 1
Entry 2
Entry 3
...
Entry 199
```

Completing entry 2 on review:

```
x Completed entry 2
x Completed entry 1
Entry 3
...
Entry 199
```

### Others

Work+Computer, Calendared, Completed, Groceries/ToBuy, Inbox

* * * * *

## Important Components of GTD System

### Notes

There are times when I clear my Inbox and some entries which do not require any actions, but looks like general information,
while still important (for some project or area) - I just move them to the `@Notes` list.

When reviewing my `@Notes` list, I could decide do I need to delete it or move to the note-taking application.
Currently I prefer [Simplenote](https://simplenote.com/) for that - very nice addition to my trusted system.

### Issue Trackers

Then working on code project, I like to treat the project bugtracker as a public context list for the project,
still having an entry for it (or better - for a single milestone of it) in the `@Projects` list.

During review, I move entries which should go to the bugtracker, to the `@@bugtracker` list.
And during review of `@@bugtracker` list, I just create issues and remove entries from Simpletask,
effectively "forgeting" about them. But I will certainly will remember them again -- then and where I resume work on the project.

| Issue tracker term        | GTD term           |
|---------------------------|--------------------|
| new issues                | inbox              |
| backlog                   | someday/maybe list |
| repository (project)      | context            |
| commit                    | action             |
| issue                     | project            |
| milestone                 | project            |

### Email

["Blue star" email parsing essay](http://roman-yagodin.github.io/how-to/2019/06/21/blue-star-email-parsing-essay) - Мanage your email inbox with 1 & ½ simple tricks.

* * * * *

## Tips & Tricks

- Simpletask provides an option to automatically generate a creation date for new tasks. Use it.
- You could make copy of entry (or entries) by sharing it. Press "Share" button and then select Simpletask as a target app.
This will produce a copy of entry with the `+background` tag.

## Issues & Problems

The following are known issues with the GTD implementation in this guide.

- __Inbox__. I enter data straight into the `todo.txt` with Simpletask or a text editor. I haven't experimented with using emails or other input, which is why I don't discuss this at all. There are some [ifttt recipes][], but I haven't tried any of them.

- __Calendar__. You do not need a calendar with this system -- at least insofar as your GTD system is concerned. Integration with an online calendar would be useful, but that is a feature that would need to be provided by Simpletask, or via something that can read the text file and populate the calendar.

- __Reference System__. This is outside the scope of a list maker such as Simpletask.

- __Project Support__. A subset of the Reference System that is related your active actions, projects, etc. There is no inherent

 I include these as "notes" (see above). For example: `2014-01-07 Complete Something or Other // Files in Dropbox > Projects > SomethingOrOther`.

- __Tickler__. The tickler system does not work all that well when you try and making it into a list. I have yet to see a virtual solution to the tickler system that work reasonably well.

- __Read/Review__.

    - "Must read" items go into the main system at the appropriate context -- since I am committed to reading or reviewing them. This works very well for items that you can keep on your mobile device.

        Example: `Read email from bank @@anywhere +finances`.

    - "Nice to read" things do not go into the main system. You might want to add some of these to your classify `@Someday` list, if you would like to review them weekly.

Since I don't care much if anything falls through the cracks, they are housed in various systems: books and movies are in text files (in a custom format, but I might convert these to the `todo.txt` format as well), online articles are in a read-it-later service, etc.

- __Performance__. Simpletask becomes quite slow if you are viewing many entries at once (over 200 on my phone). You might want to experiment with breaking off the `@Someday/Maybe` entries into their own todo file.

    That said, my `todo.txt` is over 400 lines and, while not snappy, is still usable.

## Software

- [Various Simpletask flavours](https://play.google.com/store/apps/developer?id=Mark+Janssen)
- [Simplenote](https://simplenote.com)

<!-- Reference Links -->

[Simpletask]: https://play.google.com/store/apps/details?id=nl.mpcjanssen.todotxtholo
[Mark Janssen]: http://mpcjanssen.nl/
[todo.txt]: http://todotxt.com/
[Alex Armstrong's work]: https://gist.github.com/alehandrof/9941620
[i29]: http://mpcjanssen.nl/tracker/issues/29
[ifttt recipes]: https://ifttt.com/search/query/todo