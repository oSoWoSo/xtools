# `xtools Collection`
 Collection of:
 - xtools – A collection of small utilities for use with XBPS (https://github.com/leahneukirchen/xtools)
 - xtools-extra (https://github.com/freddylist/xtools-extra)
 - xxtools (https://github.com/Piraty/xxtools)
 - xbps-src framework (https://github.com/freddylist/xbps-src-framework)

---------------------------------------

# `xtools` – A collection of small utilities for use with XBPS

### COMMANDS

`xbarf`
        – Display build logs of last build

`xbuildbarf [arch]`
        – Spy on current buildbot output

`xbulk [-n] [-k] [xbps-src flags] pkgs ...`
        – simple XBPS bulk builder
          -n  dry-run mode
          -k  keep going on errors

`xbump pkgname [git commit options]`
        – git commit a new package or package update

`xchangelog template | pkgname`
        – open package changelog

`xcheckmypkgs [email]`
        – check your packages for updates

`xcheckrestart [-v]`
        – list programs using outdated libraries
          -v  verbose mode, also print the library names

`xchroot directory [command ...]`
        – chroot into a Void (or other Linux) installation

`xclash`
        – detect file conflicts between XBPS packages

`xdbg pkgs ...`
        – list debugging packages for pkgs and recursive dependencies

`xdiff [-u | -l] [basedir]`
        – merge/diff/list XBPS .new-* files
          -l  list .new files
          -u  print unified diffs

`xdistdir`
        – figure out XBPS_DISTDIR

`xdowngrade pkgfiles.xbps ...`
        – install XBPS package directly from .xbps file

`xetcchanges``
        – show diff of /etc against binary packages

`xgensum [-f] [-c] [-i] [-H hostdir] template`
        – update SHA256 sum in templates
          -f  force (re-)download of distfiles
          -c  use content checksum
          -i  replace checksum in-place
          -H  absolute path to hostdir

`xgrep pattern pkgs ...`
        – search files limited to XBPS package contents

`hog`
        – list installed XBPS packages ordered by size

`xi pkgs ...`
        – like ‘xbps-install -S’, but take cwd repo and sudo/su into account

`xilog [pattern]`
        – list installed packages by install-date

`xlg pkg`
        – open short commit log for XBPS template

`xlint template | pkgname | :pkgname | :`
        – scan XBPS template for common mistakes
        - use ‘:pkgname’ to lint template as staged in the git index
        - use ‘:’ to lint all templates staged in the git index

`xlocate -g | -S | pattern`
        – locate files in all XBPS packages
          -g  Update a git based xlocate database, useful for local
              repositories
          -S  Sync with the official git based xlocate database, which is
              recommended before using the tool

`xlog pkg`
        – open commit log for XBPS template

`xls pkg ...`
        – list files contained in pkg (including binpkgs)

`xmandoc manpage`
        – read manpage of possibly not installed package

`xmksv [-l] [newsvdir ...]`
        – create new runit service templates. Also creates log service if -l
        is passed.

`xmypkgs [email]`
        – list all pkgs maintained by you

`xnew [-a] pkg [subpkgs ...]`
        – create XBPS template
          -a  append subpkgs to existing pkg

`xnodev`
        – list not installed -devel packages for installed packages

`xoptdiff [-q] [pkgs ...]`
        – show template options which differ from binary package
          -q  quiet mode, show package names only

`xpcdeps pcfile ...`
        – finds package matching the Requires: section of pkg-config files

`xpkg [-amOHDvV] [-r rootdir] [-R repo]`
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

`xpkgdiff [-Sfrxt] [-a arch] [-R url] [-c file] [-p prop,...] pkg`
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

`xpstree`
        – display tree view of xbps-src processes

`xq [-R] pkg ...`
        – query information about XBPS package
          -R  query remote repos

`xrecent [repourl | arch]`
        – list packages in repo ordered by build date

`xrevbump message templates ... [-- git commit options]`
        – increase template revision and commit. Use ‘-’ to read templates
        from stdin.

`xrevshlib package`
        – list packages shlib-dependent on package or its subpackages

`xrs pattern`
        – like xbps-query -Rs, but take cwd repo into account

`xsrc pkg`
        – list source files for XBPS template

`xsubpkg [-m] pkg`
        – list all subpackages of a package
          -m  only print main package

`xuname`
        – display system info relevant for debugging Void

`xvoidstrap dir [packages]`
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

# `xxtools`

Collection of tools to ease package maintenance for Void Linux even more than
xtools does.

* `xxadopt [-f] PKG..` - adopt packages
* `xxautobump PKG..` - perform trivial updates on given templates
* `xxbuild [flags] [pkgs..]` - build packages for many archs
* `xxcheckorphans` - update-check installed packages that no ones looks after

## License

[0BSD](https://spdx.org/licenses/0BSD.html), see [LICENSE](./LICENSE).

# `xbps-src framework`

Framework/glue for working with `xbps-src` to bulk build packages from custom and restricted templates.
You can aggregate templates from multiple sources, updating all of them at once (probably with a `git pull`).
See [known template collections](#known-template-collections) for a list of links to collections of templates I could find all around the interwebs.
Please open a pull request if you have more!

See also [the-maldridge/xbps-mini-builder](https://github.com/the-maldridge/xbps-mini-builder).

## Requirements

- `bash`
- GNU `make`
- `xtools`
- [`xtools-extra`](https://github.com/freddylist/xtools-extra)
	- Automatically downloaded if you have an internet connection.

### Install all requirements:
```
# xbps-install -S bash make xtools
```

## Usage

1. Clone this repository:
```
$ git clone https://github.com/freddylist/xbps-src-framework.git
```
2. Create an `xbps-src.conf` to your liking:
	- `cp xbps-src.conf.sample xbps-src.conf`
	- I recommend having the following set:
	```
	XBPS_MIRROR=https://repo-fastly.voidlinux.org/current
	XBPS_CCACHE=yes
	```
	This makes `xbps-src` use the faster Fastly CDN mirror and enables CCache. Just remember to install the `ccache` package!
	- You can also add build options here:
	```
	# Global build options
	XBPS_PKG_OPTIONS=opt,~opt2,opt3,~opt4

	# Per-package build options
	XBPS_PKG_OPTIONS_foo=opt,~opt2,opt3,~opt4
	```
3. Create directory named `srcpkgs` next to the makefile.
3. Symlink or move packages that you wish to build on `make pkgs` to the `srcpkgs` directory.
	- Don't symlink subpackages. If you need to build a subpackage, symlink the main package. Subpackages are always created with the main package, whether you want them to or not.
4. Run `make pkgs` or `make <pkgname>`.
	- Run `make sign` to sign all repositories and packages.
5. Run `make install` to install repository configuration.
	- This allows you to use `xbps-install` without `--repository=path/to/hostdir/binpkgs`.

From there, you can have a cron/snooze job occasionally update template sources and build symlinked packages for you.

If something's borked, you can try `make clean`.

Do not be afraid to open an issue if something is unclear or doesn't work.

## Known template collections

Somewhat alive:
- [freddylist/antivoid-packages](https://github.com/freddylist/antivoid-packages)
- [ayoubelmhamdi/void-linux-templates](https://github.com/ayoubelmhamdi/void-linux-templates)
- [Elvyria/voids-package-nightmare](https://github.com/Elvyria/voids-package-nightmare)
- [sug0/voided-packages](https://github.com/sug0/voided-packages)
- [mobinmob/abyss-packages](https://codeberg.org/mobinmob/abyss-packages)
- [DAINRA/ungoogled-chromium-void](https://github.com/DAINRA/ungoogled-chromium-void)
- [Marcoapc/voidxanmodK](https://notabug.org/Marcoapc/voidxanmodK)
- [weebi/void-packages](https://github.com/weebi/void-packages)

Seem to be kinda dead:
- [fdziarmagowski/into-the-void](https://github.com/fdziarmagowski/into-the-void)
- [cadadr/void-packages](https://codeberg.org/cadadr/void-packages)
- [reback00/void-goodies](https://notabug.org/reback00/void-goodies/src/master)
- [oSoWoSo/nvoid](https://github.com/oSoWoSo/nvoid), forked from [not-void/nvoid](https://github.com/not-void/nvoid)
- [70xH/void-kernel-builds](https://github.com/70xH/void-kernel-builds)
- [gbrlsnchs/void-pkgs](https://github.com/gbrlsnchs/void-pkgs)
- [nereusx/void-extra](https://github.com/nereusx/void-extra)
- [notchtc/custom-void-packages](https://github.com/notchtc/custom-void-packages)
- [intrnl/custom-void-packages](https://codeberg.org/intrnl/custom-void-packages)

## References

* https://github.com/void-linux/void-packages
* https://github.com/leahneukirchen/xtools
* https://github.com/freddylist/xtools-extra
* https://github.com/Piraty/xxtools
* https://github.com/freddylist/xbps-src-framework

