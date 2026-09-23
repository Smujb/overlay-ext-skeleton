# Local Sysext Skeleton

> [!WARNING]
> This repository is not meant to be used directly by end users, but to be pulled in by another tool I have not yet made public.

This mkosi profile is designed to be used for building overlays on systemd-sysupdate systems which are already booted. Right now, it specifically targets the usecase where the image was built on a specific version of the Arch Linux Archive, but there are probably other ways of acheiving this reliably.

# Known Limitations

Obviously, if you cannot guarantee packages installed in this way will be syncronized with the base system with no layered updates then this tool will not work correctly or perhaps even at all.

This project requires your `/usr/lib/os-release` file to contain the variable `IMAGE_SNAPSHOT=` set to the snapshot of the package db that the image was built against. This will be passed directly to mkosi, and the format may depend on the distribution used (Arch is `YYYY/MM/DD` for example).

Ideally this would be fixed by pacman - we would rather not assume a versioning scheme or package manager.

Additionally, package metadate for the base image is assumed to be in `/usr/lib/sysimage/lib/pacman`. This is hacky and [can hopefully be addressed by mkosi](https://github.com/systemd/mkosi/discussions/4459). Currently, package db info from the overlay does not persist onto the final image but again this would be fixed if mkosi implements custom db paths.

Currently, some post-install scripts will fail to run if they are provided by a package already present on the image but required by one installed on the overlay. This issue is being tracked [here](https://github.com/systemd/mkosi/issues/4461).
