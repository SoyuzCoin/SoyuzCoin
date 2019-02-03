
Debian
====================
This directory contains files used to package soyuz3d/soyuz3-qt
for Debian-based Linux systems. If you compile soyuz3d/soyuz3-qt yourself, there are some useful files here.

## soyuz3: URI support ##


soyuz3-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install soyuz3-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your soyuz3qt binary to `/usr/bin`
and the `../../share/pixmaps/soyuz3128.png` to `/usr/share/pixmaps`

soyuz3-qt.protocol (KDE)

