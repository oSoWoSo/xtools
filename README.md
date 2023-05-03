# xtools

XTOOLS(1)                   General Commands Manual                  XTOOLS(1)

NAME
     xtools – A collection of small utilities for use with XBPS

COMMANDS
     xbarf
        – Display build logs of last build

     xbuildbarf [arch]
        – Spy on current buildbot output

     xbulk [-n] [-k] [xbps-src flags] pkgs ...
        – simple XBPS bulk builder
          -n  dry-run mode
          -k  keep going on errors

     xbump pkgname [git commit options]
        – git commit a new package or package update

     xchangelog template | pkgname
        – open package changelog

     xcheckmypkgs [email]
        – check your packages for updates

     xcheckrestart [-v]
        – list programs using outdated libraries
          -v  verbose mode, also print the library names

     xchroot directory [command ...]
        – chroot into a Void (or other Linux) installation

     xclash
        – detect file conflicts between XBPS packages

     xdbg pkgs ...
        – list debugging packages for pkgs and recursive dependencies

     xdiff [-u | -l] [basedir]
        – merge/diff/list XBPS .new-* files
          -l  list .new files
          -u  print unified diffs

     xdistdir
        – figure out XBPS_DISTDIR

     xdowngrade pkgfiles.xbps ...
        – install XBPS package directly from .xbps file

     xetcchanges
        – show diff of /etc against binary packages

     xgensum [-f] [-c] [-i] [-H hostdir] template
        – update SHA256 sum in templates
          -f  force (re-)download of distfiles
          -c  use content checksum
          -i  replace checksum in-place
          -H  absolute path to hostdir

     xgrep pattern pkgs ...
        – search files limited to XBPS package contents

     xhog
        – list installed XBPS packages ordered by size

     xi pkgs ...
        – like ‘xbps-install -S’, but take cwd repo and sudo/su into account

     xilog [pattern]
        – list installed packages by install-date

     xlg pkg
        – open short commit log for XBPS template

     xlint template | pkgname | :pkgname | :
        – scan XBPS template for common mistakes
        - use ‘:pkgname’ to lint template as staged in the git index
        - use ‘:’ to lint all templates staged in the git index

     xlocate -g | -S | pattern
        – locate files in all XBPS packages
          -g  Update a git based xlocate database, useful for local
              repositories
          -S  Sync with the official git based xlocate database, which is
              recommended before using the tool

     xlog pkg
        – open commit log for XBPS template

     xls pkg ...
        – list files contained in pkg (including binpkgs)

     xmandoc manpage
        – read manpage of possibly not installed package

     xmksv [-l] [newsvdir ...]
        – create new runit service templates. Also creates log service if -l
        is passed.

     xmypkgs [email]
        – list all pkgs maintained by you

     xnew [-a] pkg [subpkgs ...]
        – create XBPS template
          -a  append subpkgs to existing pkg

     xnodev
        – list not installed -devel packages for installed packages

     xoptdiff [-q] [pkgs ...]
        – show template options which differ from binary package
          -q  quiet mode, show package names only

     xpcdeps pcfile ...
        – finds package matching the Requires: section of pkg-config files

     xpkg [-amOHDvV] [-r rootdir] [-R repo]
        – convenient package lister
          -a  list all packages (default: only installed)
          -m  list manual packages
          -O  list orphaned packages
          -H  list packages on hold
          -D  list installed packages not in repo
          -L  list installed packages not from remote repos
          -v  show version numbers
          -V  show version numbers and description
          -r rootdir
              specifies a full path for the target root directory
          -R repo
              consider only packages from repo

     xpkgdiff [-Sfrxt] [-a arch] [-R url] [-c file] [-p prop,...] pkg
        – compare a package in the repositories to the locally-built version
        - run from within a void-packages checkout
        - set DIFF to change the diff program used
          -S  compare package metadata
          -f  compare package file lists
          -r  reverse diff (compare local to remote)
          -x  compare package dependencies
          -t  compare the full package dependency tree.  Only used with -x
              (equivalent to xbps-query --fulldeptree -x)
          -a arch
              set architecture for comparison
          -R url
              set remote repository url
          -c file
              compare a file from the package (equivalent to xbps-query --cat)
          -p prop,...
              compare properties of the package

     xpstree
        – display tree view of xbps-src processes

     xq [-R] pkg ...
        – query information about XBPS package
          -R  query remote repos

     xrecent [repourl | arch]
        – list packages in repo ordered by build date

     xrevbump message templates ... [-- git commit options]
        – increase template revision and commit. Use ‘-’ to read templates
        from stdin.

     xrevshlib package
        – list packages shlib-dependent on package or its subpackages

     xrs pattern
        – like xbps-query -Rs, but take cwd repo into account

     xsrc pkg
        – list source files for XBPS template

     xsubpkg [-m] pkg
        – list all subpackages of a package
          -m  only print main package

     xuname
        – display system info relevant for debugging Void

     xvoidstrap dir [packages]
        – bootstrap a new Void installation

DESCRIPTION
     Tools working on the void-packages tree use xdistdir to find it, check
     that its output is reasonable first.

     xi, xls, xq and xrs prefer the hostdir / binpkgs repo if you run them
     from a void-packages checkout.

LICENSE
     xtools is in the public domain.

     To the extent possible under law, the creator of this work has waived all
     copyright and related or neighboring rights to this work.

     http://creativecommons.org/publicdomain/zero/1.0/

BUGS
     All bugs should be reported to https://github.com/leahneukirchen/xtools

Void Linux                       June 25, 2019                      Void Linux

# `xtools-extra`

Extra [`xtools`](https://github.com/leahneukirchen/xtools)-style scripts.

## Requirements

- `xtools`

## Usage

### xpunt

```
xpunt [path/to/pkg...]
```

Punt packages into `${XBPS_DISTDIR}/srcpkgs` if not already there.

### xupdate

```
xupdate [-H <hostdir>] [-f] <template>
```

- `-H <hostdir>` hostdir to pass to `xgensum`
- `-f` force generating checksum
- `<template>` path to template

`xupdate` will move templates (and `update` files) to `${XBPS_DISTDIR}/srcpkgs` if not already there. Then it will try to heuristically detect new versions for given templates, bump the version of the template and generate the checksum for new distfiles. Afterwards, it will move the updated template back to its original location.

### xwrapper

```
xwrapper [xbps-src options] [xbps-src target] [name or path to package]
```

`xwrapper` will `xpunt` given packages, then invoke `xbps-src` with whatever options you gave.

# xxtools

Collection of tools to ease package maintenance for Void Linux even more than
xtools does.

* `xxadopt [-f] PKG..` - adopt packages
* `xxautobump PKG..` - perform trivial updates on given templates
* `xxbuild [flags] [pkgs..]` - build packages for many archs
* `xxcheckorphans` - update-check installed packages that no ones looks after

## License

[0BSD](https://spdx.org/licenses/0BSD.html), see [LICENSE](./LICENSE).

## References

* https://github.com/void-linux/void-packages
* https://github.com/leahneukirchen/xtools

