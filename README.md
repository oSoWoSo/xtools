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
