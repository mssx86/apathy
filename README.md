### msslinux-pure64 build details
mssLinux is a pure 64bit linux distribution built by following *linux from scratch 8.4* and *beyond linux from scratch 8.4* books. i have also used multiple `pkgbuild`'s from arch linux official repositories and `aur`, there have been times where i used gentoo `ebuild`'s to check build flags and dependencies using `use` flags as well.

this is the third *release* of mssLinux, 1.0 being my first experience with lfs. my first attempt felt really bloated so i wanted to make a second attempt but also with 32bit libraries, that got out of hand real quick so i gave up on a multilib build.

complete list of software/packages installed can be found in `raw-packages.txt` or `packages.md`, under the `lists` directory. the configuration files used to set up or compile software is under the `build-config-and-misc` directory.

![yes](assets/fetch.png)

#### current package count:
```
[18:46] mss mssLinux [master][*]: wc -l pkg-management/raw-packages.txt 
391 pkg-management/raw-packages.txt
```
