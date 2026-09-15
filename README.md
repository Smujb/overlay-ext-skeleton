# Local Sysext Skeleton

> [!WARNING]
> This repository is not meant to be used directly by end users, but to be pulled in by another tool I have not yet made public.

This mkosi profile is designed to be used for building overlays on systemd-sysupdate systems which are already booted. Right now, it specifically targets the usecase where the image was built on a specific version of the Arch Linux Archive, but there are probably other ways of acheiving this reliably.

# Known Limitations

Obviously, if you cannot guarantee packages installed in this way will be syncronized with the base system with no layered updates then this tool will not work correctly or perhaps even at all.

Currently, this project is hard tied to a versioning scheme where the first 8 digits of the version make up the date of the Arch Linux Archive build used to build this image (YYYYMMDD). Other ways of syncronizing package metadata are not supported, but hopefully will be in future.

Ideally this would be fixed by pacman - we would rather not assume a versioning scheme or package manager.

Additionally, package metadate for the base image is assumed to be in `/usr/lib/sysimage/lib/pacman`. This is hacky and [can hopefully be addressed by mkosi](https://github.com/systemd/mkosi/discussions/4459). Currently, package db info from the overlay does not persist onto the final image but again this would be fixed if mkosi implements custom db paths.
