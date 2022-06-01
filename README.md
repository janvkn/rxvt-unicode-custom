# rxvt-unicode-custom

This repository contains a PKGBUILD file to create my personally customized rxvt-unicode and rxvt-unicode-terminfo packages for Arch Linux.

The PKGBUILD file was forked from the official Arch Linux PKGBUILD file for rxvt-unicode, which you can find here: https://github.com/archlinux/svntogit-community/tree/packages/rxvt-unicode/trunk

It also includes a few bits from the now defunct [rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched) AUR package.

The main differences with the official PKGBUILD are:

* Updated the version to the latest upstream version of rxvt-unicode: 9.30
* Added dependency to [libptytty](https://aur.archlinux.org/packages/libptytty), which is needed for 9.30.
* Re-enabled some frills in the configure script
* Integrated the font-width-fix patch
* Integrated the line-spacing-fix patch

The generated packages are called `rxvt-unicode-custom` and `rxvt-unicode-custom-terminfo`. They will conflict with the official packages, so you will be prompted to uninstall them.