# Ved's build of dwm

dwm is an extremely fast, small, and dynamic window manager for X.


## Bindings
Custom bindings are commented in the config headers [config.def.h](config.def.h).

## Patches

Patches in this build are stored in /patch. They can be looked up on https://dwm.suckless.org/patches/

- cfacts-vanitygaps-6.2_combo: assign weights to clients within their stack in the layout
- systray-6.3: a system tray implementation in dwm
- nametag-prepend-6.2: allow custom text to be appended to tag numbers `super + n`
- alternativetags-6.3: hold `super + shift + a` to view alternate tags
- movestack-20211115-a786211: move clients up/down the stack
- cyclelayouts-20180524-6.2: cycle through all layouts available `super + shift + comma`
- hide_vacant_tags-6.3: hide tags with no windows for a cleaner bar
- pertag-20200914-61bb8b2: allow setting different layouts for unique tags
- autostart-20210120-cb3f58a: loads up commands in ~/.dwm/autostart.sh
- barpadding-20211020-a786211: add horizontal/vertical padding to the status bar
- actualfullscreen-20211013-cb3f58a: force a window to go fullscreen and hide the statusbar `super + f`
- restoreafterrestart-20220709-d3f93c7: maintain client/tag ordering upon restarting dwm
- restartsig-20180523-6.2: kill & restart dwm without logging out - useful post compilation. `super + ctrl + shift + q`
- xresources-20210827-138b405: compatibility with settings in .xresources
- rebootcmd-20220202-d39e2f3: reboot the system `super + shift + delete`
- shutdowncmd-20220202-d39e2f3: shutdown the system `super + shift + escape`
- namedscratchpads-6.2: multiple scratchpads on their respective keys
- swallow-6.3: swallow floating windows that spawn from a terminal (i.e. hide parent process)

manual fixes applied:
1. [systray/barpadding compatibility][1]
	 patch summarised below -
	```
	- XMoveResizeWindow(dpy, systray->win, x, m->by , w, bh);
	- wc.x = x ; wc.y = m->by ; wc.width = w; wc.height = bh;`
	+ XMoveResizeWindow(dpy, systray->win, x - sp, m->by + vp, w, bh);
	+ wc.x = x - sp; wc.y = m->by + vp; wc.width = w; wc.height = bh;
	```

## Requirements
In order to build dwm you need the Xlib header files. These should be available in your distribution's Xorg package.

## Installation

Edit config.mk to match your local setup (dwm is installed into
the /usr/local namespace by default).

```
git clone https://github.com/shastryv/dwm
cd dwm
rm config.h && sudo make clean install
```


## Usage
Add the following line to your .xinitrc to start dwm using startx:

```
    exec dwm
```

## Links
[1]: https://www.reddit.com/r/suckless/comments/sgdpqz/comment/i6hb2ce/?utm_source=share&utm_medium=web2x&context=3
