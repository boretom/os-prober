Debian's os-prober used by `update-grub`, based on version 1.77 from
[Debian Installer Git Repo](https://salsa.debian.org/installer-team/os-prober).
With patches added from [Fedora 32 package](https://src.fedoraproject.org/rpms/os-prober)

## Why ##
Linux Mint 19 and Linux Mint 20 Beta didn't find each other while running `update-grub` on a Intel NUC with legacy boot
disabled. And therefore I had to manually add the entries to `grub.d/40_custom`. Both distros were installed on btrfs,
one with a non-standard rootfs name. `os-prober` not finding them in 2020 that is ... mmmh ... unexpected ... and here we are.

## How ##
If you trust me enough then download the latest `*.deb` file from the 'release' page.

If you'd like to create the `*.deb` file yourself:

0. Be on Linux Mint 19 or 20 (I assume Ubuntu 20 or one before will work too, or Debian but not tested)
1. Install necessary packages: `sudo apt install gnupg apt-file debhelper`
2. Clone this repo and `cd` into it
3. Apply patches:

    `for p in ./debian/patches/*.patch; do patch -p1 < $p; done`
 
4. Create the package: `dpkg-buildpackage -us -ui -uc`
5. Install the created package: `sudo dpkg -i ../os-prober_1.77+nmu1_amd64.deb
6. Run `sudo os-prober` to check if your linux distro where found

Disclaimer: As always no garantuee and if it breaks it wasn't me. All praise to the original authors of the patches which
are not named in them so not sure who to thank.
