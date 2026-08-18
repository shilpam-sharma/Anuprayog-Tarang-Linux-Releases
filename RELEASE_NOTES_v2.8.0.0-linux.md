# AnuPrayog: Tarang (Linux) v2.8.0.0

The first Linux release — an AppImage built from the same v2.8.0.0
codebase as the [Windows release](https://github.com/shilpam-sharma/Anuprayog-Tarang-Releases/releases/tag/v2.8.0.0),
carrying the same feature set (the RF/Microwave Suite plugin, the
`.trg` project format, the new application icon — see that release's
notes for details).

## Getting started

```bash
chmod +x AnuPrayog_Tarang-2.8.0.0-x86_64.AppImage
./AnuPrayog_Tarang-2.8.0.0-x86_64.AppImage
```

No installation needed. Requires glibc 2.35+ (Ubuntu 22.04+, Debian 12+,
Fedora 36+ and most actively-supported distros as of 2026) — it will not
run on Ubuntu 20.04 or Debian 11.

## What's Linux-specific about this build

- `.opj` Origin-file import works via a Linux build of the open-source
  `liborigin` parser (GPLv3), rebuilt from the same source the Windows
  build uses — not a stub or a degraded fallback.
- Packaged with [linuxdeploy](https://github.com/linuxdeploy/linuxdeploy)
  and bundles its own copy of Qt's platform-integration libraries, so it
  doesn't depend on what's already installed on your system.
- `.trg`/`.anu` double-click file association isn't wired up yet — open
  files from within the app for now (**File > Open Project**).

## Known limitations of this first release

- Verified extensively through this project's own automated test suite
  (which drives the real Qt/matplotlib rendering pipeline headlessly)
  and manual smoke testing, but **not yet visually confirmed running on
  a real Linux desktop** — the build environment used to produce this
  release has host-level graphics driver limitations that prevent a
  visual check there specifically. If you hit a display issue, please
  open an issue on this repository.
