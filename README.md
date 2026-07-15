# Smart Mirror

A DIY smart mirror built around a Raspberry Pi 5, running MagicMirror2 behind a custom two way mirror surface housed in a wood frame.

# What it does

The mirror boots straight into a portrait oriented display showing time, date, weather, calendar, and news, with no monitor or keyboard needed after initial setup. It runs fully headless, launching itself automatically every time it powers on.

# Hardware

* Wood plank (wide) and wood plank (narrow) for the frame
* Clear acrylic sheet as the mounting substrate
* Gila window film applied over the acrylic to create the two way mirror effect
* Monitor, roughly 21 by 13 inches, mounted behind the film and rotated to portrait
* Raspberry Pi 5, 2GB RAM
* 64GB microSD card
* USB C power supply rated for the Pi 5 (5V/5A, 27W)
* Micro HDMI to HDMI cable

# Software

* Raspberry Pi OS, 64 bit, Desktop edition
* Node.js 22
* MagicMirror2, installed from the official MagicMirrorOrg repository
* labwc as the desktop compositor, used to rotate the display and to launch MagicMirror automatically on boot

# How the display rotation works

The Pi's desktop session runs on Wayland through labwc. MagicMirror itself runs through Xwayland using its start:x11 mode, since the native Wayland launch had rendering issues on this hardware. Rotating the actual screen output has to happen at the compositor level with wlr randr, since xrandr only talks to the Xwayland layer and cannot resize the real screen.

Both the rotation command and the MagicMirror launch command live in labwc's autostart file, so everything comes up correctly oriented with zero manual steps after power on.

# Repo contents

* MATERIALS.txt, full parts list
* BUILD_COMMANDS.txt, the complete chronological command log used to set this build up, including the real troubleshooting along the way (PM2 not launching GUI apps, xrandr failing under Wayland, the fix using wlr randr and labwc autostart)
* config.js, the MagicMirror configuration used for this build
* custom.css, any layout tweaks made for portrait mode
* autostart, the labwc file that rotates the screen and launches MagicMirror on boot
* images/, build and finished photos
* video/, a demo clip of the mirror running

# Notes

This was built and documented as a portfolio project alongside embedded systems work on the Raspberry Pi platform. The build log intentionally keeps the dead ends in, since the debugging process (figuring out why PM2 could not launch a GUI app, or why xrandr kept failing until wlr randr was used instead) is as much a part of the project as the finished result.

Notes

This was built and documented as a portfolio project alongside embedded systems work on the Raspberry Pi platform. The build log intentionally keeps the dead ends in, since the debugging process (figuring out why PM2 could not launch a GUI app, or why xrandr kept failing until wlr randr was used instead) is as much a part of the project as the finished result.
