```


   __,  ,_   __,  -/- /_
  (_/(__/_)_(_/(__/__/ (__(_/_
       /                  _/_
      /                  (/

apathy is a linux "distribution" built on top of apathy-mlfs, which can be
found at https://github.com/mssx86/apathy-mlfs, for my own purposes. it uses
musl libc, libressl, partially busybox and a home-brewed init structure written
in posix shell.

because it is intended for my use only, this repository does not contain an
image to boot from or a stage3 tarball to unpack, though it is possible to
build a system using the base that apathy uses.


simplified list of major components
===================================
 > toolchain
   - musl 1.2.0       - binutils 2.34      - gcc 10.1.0
   - mpfr 4.0.2       - gmp 6.2.0          - mpc 1.1.0 
   - musl-fts 1.2.7   - musl-obstack 1.1   - argp-standalone 1.3
   - gcompat 0.4.0    - libucontext 0.1.3

   - python 2.7.1     - python 3.8.2       - lua 5.2.4
   - perl 5.30.1

 > toolchain (ondemand)
   - llvm-10.0.0      - clang-10.0.0       - rustc-1.43.1
   - cbindgen-0.14.2  - go-1.14.1          - node.js-13.9.0
   - boost 1.72.0

 > core userland
   - util-linux 2.35  - coreutils 8.32     - busybox 1.31.1
   - sysklogd 1.5.1   - sinit 1.1          - eudev 3.2.9
   - yash 2.49

 > tls
   - libressl 3.2.0   - gnutls-3.6.13      - nettle-3.5.1


simplified repository tree
==========================
 .
 ├─ ainit-initbits ──────────────> my init system written in posix shell, using
 │                                 sinit+sbase+ubase.
 ├─ apathy-utils ────────────────> many small utilities used in apathy, written
 │                                 in posix shell.
 ├─ directories
 │  ├─ personal ─────────────────> personal configuration files.
 │  └─ system ───────────────────> base system configuration files that goes
 │                                 under /etc and /usr. 
 ├── misc
 │   ├─ ainit-sysv
 │   │   ├─ ainit-sysv-mk-i ─────> a posixified version of lfs-bootscripts,
 │   │   │                         used when the system was called mssLinux.
 │   │   └─ ainit-sysv-mk-ii ────> first from-scratch init system, using gnu
 │   │                             coreutils and sysvinit.
 │   └─ g3258-memorial ──────────> notes and details saved from my old system
 │                                 where i built almost everything on.
 └─── pkg-management
     ├─ packages.md ─────────────> a formatted list of all installed, removed 
     │                             and ondemand packages with extra notes about
     │                             the installation/removal process.
     ├─ raw-packages.txt ────────> list of all installed programs in plain
     │                             unformatted text.
     ├─ installation-details ────> directory listings of installed programs.
     ├─ removal-details ─────────> directory listings of removed programs.
     ├─ build-configs ───────────> custom home-brewed build recipes for a
     │   │                         variety of software.
     │   └─ www-browser
     │       └─ apathy-browser ──> pale moon fork with custom branding and
     │                             uaoverrides/prefs.js.
     └─ patches ─────────────────> patches to be used with recipes under
                                   build-configs/.


history
=======
versioning is done solely for defining the "era" of apathy that used different
compontents, it does not mean anything.

    1. mssLinux 1.1, apathy gnu/linux 1.{2,3}:
       - it initially used linux from scratch 8.4 as its base and the rest was
         built off of reading gentoo ebuild's and arch linux PKGBUILDS.
       - first iterations of utilities under apathy-utils/ is written here.
         same goes for ainit-sysv-mk-i which is just a posixified version of
         lfs-bootscripts so that i could boot with dash.
       - latest state of this "release" can be found at the apathy-glibc branch
         of this repo.

    2. apathy musl 1.0
       - it used "mlfs" written by github user dslm4515 as its base and the
         rest was built off of reading alpine APKBUILD's.
       - pretty much everything else is straight from the glibc apathy.

    3. apathy musl 1.1
       - i forked mlfs to apathy-mlfs. cleaned up the documentation, simplified
         things, changed the shells, the init system, updated majority of the
         software alongside with patches, and used it as the base for this
         "release".
       - pretty much everything else is the same as the previous mlfs based
         system.

    4. apathy musl 1.2 - part 1
       - having sold my g3258 and bought a thinkpad t61, i decided on
         rebuilding the system as the previous haswell chip had instructions
         that my core2 duo in the t61 didn't have.
       - the `init-functions` and `rc` from lfs-bootscripts got rewritten and
         named `ainit-sysv-mk-ii`. instead of doing runlevel based symlinking,
         now `rc` handled everything by case statements. the whole structure
         got much more portable to move between init's.

    5. apathy musl 1.2 - part 2
       - i removed the runlevel management bits from rc and moved the already
         portable ainit-sysv-mk-ii to sinit. instead of util-linux and coreutils
         bits, i used components from static sbase and ubase builds.
       - at this stage, instead of blindly taking the build recips from alpine,
         i started trimming down the fat and writing my own recipes more. the
         size of the distribution went down from 1450mib to 960mib without
         losing functionality.
```
