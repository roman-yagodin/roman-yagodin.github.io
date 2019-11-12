---
layout: post
category: guide
title: "Arcanum on Linux with Steam Play Proton"
tagline: "plus UAP and HighRes patches"
tags : [games, linux, steam, proton, wine]
---
{% include JB/setup %}

Celebrating recent update to [Unofficial Arcanum Patch][] after almost 10 years since the last one, I decided to write this post to guide you through the basics of install and setup process of famous [Arcanum: Of Steamworks and Magick Obscura][] title on Linux with the Steam Play [Proton][].

<!-- more -->

<img src="{{ site.url }}/assets/images/arcanum-library.png" alt="Arcanum in Steam library" class="img-responsive" />

## Proton and Steam Play

[Proton][] is compatibility tool for [Steam Play][] based mainly on *Wine* plus some other components like *DXVK*. It allows you to install and run Windows games via Steam client on "unsupported" platforms - almost like a native games. While you still can install any game from your Steam library on Linux with [steamcmd][], and then use *Wine*, *Winetricks* or e.g. [PlayOnLinux][] to run it, the *Proton* provides very refreshing and more straightforward alternavite.

The *Proton* doesn't looks very mature for the moment, but it contantly improves. User reports about various games are gathered in the [ProtonDB][] (its like the [WineHQ][] is for *Wine*), there you can find useful tips on how to setup your favorite game or which quirks to expect from it. You can also find the growing list of [whitelisted][] games there.

## General sequence

1. Install the game.
2. Setup *wineconsole*.
3. Install *Unofficial Arcanum Patch*.
4. Apply *HighRes* patch.
5. Play.

## Install the game

First of all, you need to enable Steam Play for all titles via *Steam client settings* / *Steam Play options*.

This will allow you to install (and run) Arcanum on Linux just like any other native Linux game from your Steam libary.

<img src="{{ site.url }}/assets/images/arcanum-enable-steam-play.png" alt="Enable Steam play for all other titles" class="img-responsive" />

After that, you can install the game by just clicking *Install*.

After installing, run game once - just to create `$HOME/.local/share/Steam/steamapps/compatdata/500810` directory.
It will take some time, as Steam will need to download *Proton* and create wineprefix for the game.

Add symlink to the game install directory and place it inside the `$HOME/.local/share/Steam/steamapps/compatdata/500810/pfx/drive_c` directory:

```shell
ln -s "$HOME/.local/share/Steam/steamapps/common/Arcanum" \
  "$HOME/.local/share/Steam/steamapps/compatdata/500810/pfx/drive_c/Arcanum"
```

**Note:** I think there should be a better way to do that (without creating symlink), as *Proton* surely do need to merge the game install directory with wineprefix somehow.
If you know something about it, please drop a comment.

## Setup wineconsole 

### Wine way

*wineconsole* is the *Wine* console manager, used to run console commands and applications. We will need it to run `cmd.exe` shell in order to run some commands to setup the game.

Execute in the terminal emulator (replace `Proton 4.11` with actual *Proton* version):

```shell
env WINEPREFIX="$HOME/.steam/steam/steamapps/compatdata/500810/pfx" \
  WINEPATH="$HOME/.local/share/Steam/steamapps/common/Proton 4.11/dist/bin/wine" \
  wineconsole
```

<img src="{{ site.url }}/assets/images/arcanum-wineconsole.png" alt="Arcanum folder via wineconsole" class="img-responsive" />

Feeling some nostalgia? It's cool!

**Note:** AFAIK this is not 100% safe way - but it will work the same for other games, which doesn't have configurable launcher.

### SierraLauncher way

Backup `SierraLauncher.ini` into `original_SierraLauncher.ini`

Create `cmd.bat` file with following content:

```
cmd.exe
```

Modify `SierraLauncher.ini`

```ini
[Launcher]
Name=Arcanum
NumButtons=1
GameManual=Manual.pdf

Game1Name=Game
Game1Prog=other
Game1Path=\
Game1Exe=cmd.bat
Game1Cmd=
```

Now run the game - it will start `SierraLauncher.exe`, but then you click *Launch*, it will open *wineconsole* (`cmd.exe`) window instead.

**Note:** Optionally you can create a `cmd_SierraLauncher.ini` file and make `SierraLauncher.ini` the symlink to it. This way you can switch between two `.ini` versions without copying files.

## Install Unofficial Arcanum Patch

Get latest and the greatest [Unofficial Arcanum patch][].

Copy *UAP* installer to the Arcanum folder.

Run *wineconsole*, type some commands:

```
C:
cd Arcanum
UAP1.5.1.exe
```

<img src="{{ site.url }}/assets/images/arcanum-uap.png" alt="Arcanum: Unofficial patch installer" class="img-responsive" />

Choose things to install - it's about your preference, but surely *HighRes* patch is greatly recommended.

About level cap remover - I think it's more fun to just start again with different kind of character.

Proceed. Select proper install location carefully: 

<img src="{{ site.url }}/assets/images/arcanum-uap-install-path.png" alt="Arcanum: Unofficial patch install path" class="img-responsive" />

Done.

## Apply HighRes patch

Then you install *Unofficial patch*, the *HighRes* patch will be installed into `Arcanum/HighRes` directory, but not applied, as it will require some additional configuration. Let's do it.

Open *HighRes* `config.ini` and modify it as you like:

```ini
Width = 1920 // original: 800
Height = 1080 // original: 600
DialogFont = 2 // 0 = size 12, 1 = size 14, 2 = size 18
```

Save changes.

Install patch. Open *wineconsole* again,  type:

```
C:
cd Arcanum\Arcanum\HighRes
_install.bat
exit
```

<img src="{{ site.url }}/assets/images/arcanum-highres-applied.png" alt="Arcanum: HighRes patch applied" class="img-responsive" />

Done.

## Play

If you started *wineconsole* from SierraLauncher, it's time to restore the `SierraLauncher.ini` to its original state.

Now **run Arcanum from your Steam library** and have fun with such a great game!

<img src="{{ site.url }}/assets/images/arcanum-in-game.png" alt="Arcanum: In game" class="img-responsive" />

For the first-timers I'd recommend to start with the [official manual](http://terra-arcanum.com/downloads/arcanum/resources/arcanum_manual.zip) or the [Spoiler-Free Character Creation Guide and Orientation (pre-UAP)][].

Please share your favorite resources for beginners in the comments!

## Troubleshooting

Unfortunately, you can experience graphics glitches (like one on the screenshot).

<img src="{{ site.url }}/assets/images/arcanum-graphics-glitch-small.png" alt="Arcanum: Graphics glitch" class="img-responsive" />

The most simple way to fix it is to switch to the software rendering via *HighRes* `config.ini`:

```ini
Renderer = 0 // 0 = software, 1 = hardware
```

Repeat *HighRes* patch setup, but run `_uninstall.bat` first.

```
C:
cd Arcanum\Arcanum\HighRes
_uninstall.bat
_install.bat
exit
```

## Additional tweaks

Before switching to software renderer, you could also explore other possibilities by tweaking some options via *HighRes* `config.ini`, [Wine](https://wiki.winehq.org/Useful_Registry_Keys) and/or [Proton](https://github.com/ValveSoftware/Proton#runtime-config-options). Feel free to share your glitches and the setup options which worked (not worked) for you in the comments.

### Setting Arcanum.exe options via SierraLauncher.ini

This is an (almost) obsolete way to do it, as the *HighRes* patch allows you to set many options via `config.ini`. But still, let's set `-doublebuffer` option:

```ini
[Launcher]
Name=Arcanum
NumButtons=1
GameManual=Manual.pdf

Game1Name=Game
Game1Prog=other
Game1Path=Arcanum\
Game1Exe=Arcanum.exe
Game1Cmd=-doublebuffer
```

See more [here](https://terra-arcanum.com/forums/index.php?threads/arcanum-command-line-arguments.15208/).

### Setting Wine options via regedit

1. Run *wineconsole*.
2. Type `regedit`.
3. Go to `HKEY_CURRENT_USER\Software\Wine\Direct3D` (if key not exists, create it).

Here you can set number of *Wine* options, like:

```
"DirectDrawRenderer"="gdi"
"OffscreenRenderingMode"="backbuffer"
```

See more [here](https://wiki.winehq.org/Useful_Registry_Keys).

### Emulate virtual desktop

1. Run *wineconsole*.
2. Type `winecfg`.
3. Go to *Graphics* tab.
4. Check *Emulate virtual desktop* option.
5. Set required values for screen width and height.
6. Ensure that same width and height values is set and also fullscreen is enabled in the *HighRes* `config.ini`.

## Finally, some links:

- [Unofficial Arcanum patch][]
- [Arcanum entry in ProtonDB](https://www.protondb.com/app/500810)
- [Terra Arcanum](http://terra-arcanum.com)
- [Official Manual](http://terra-arcanum.com/downloads/arcanum/resources/arcanum_manual.zip)
- [Spoiler-Free Character Creation Guide and Orientation (pre-UAP)][]
- [Proton runtime config options](https://github.com/ValveSoftware/Proton#runtime-config-options)
- [Wine useful registry keys](https://wiki.winehq.org/Useful_Registry_Keys)
- [Proton code repository on GitHub](https://github.com/ValveSoftware/Proton)
- ["whitelisted" ProtonDB games](https://www.protondb.com/explore?page=0&selectedFilters=whitelisted)
- [Arcanum.exe commandline arguments](https://terra-arcanum.com/forums/index.php?threads/arcanum-command-line-arguments.15208/)
  
<!-- Reference Links -->

[Arcanum: Of Steamworks and Magick Obscura]: https://store.steampowered.com/app/500810/Arcanum_Of_Steamworks_and_Magick_Obscura/
[Spoiler-Free Character Creation Guide and Orientation (pre-UAP)]: https://gamefaqs.gamespot.com/pc/914155-arcanum-of-steamworks-and-magick-obscura/faqs/64280
[Unofficial Arcanum Patch]: http://terra-arcanum.com/drog/uap.html
[Steam Play]: https://steamcommunity.com/games/221410/announcements/detail/1696055855739350561
[ProtonDB]: https://www.protondb.com
[Proton]: https://github.com/ValveSoftware/Proton
[WineHQ]: https://www.winehq.org
[PlayOnLinux]: https://www.playonlinux.com
[steamcmd]: https://developer.valvesoftware.com/wiki/SteamCMD
[whitelisted]: https://www.protondb.com/explore?page=0&selectedFilters=whitelisted
