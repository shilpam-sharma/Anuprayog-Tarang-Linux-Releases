# AnuPrayog: Tarang — Linux

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21988908.svg)](https://doi.org/10.5281/zenodo.21988908)

A scientific data analysis and plotting application.

**Downloads:** see [Releases](https://github.com/shilpam-sharma/Anuprayog-Tarang-Linux-Releases/releases) — an
[AppImage](https://appimage.org/) is attached to each release. Download it, `chmod +x`, and run —
no installation needed. Requires glibc 2.35+ (Ubuntu 22.04+, Debian 12+, Fedora 36+ and most
actively-supported distros).

Free to use, closed source. See the EULA for full terms.

This is a Linux build of the same [AnuPrayog: Tarang](https://github.com/shilpam-sharma/Anuprayog-Tarang-Releases)
that ships for Windows, built from the same codebase. See "How this differs from the Windows build" below for
what's platform-specific.

## Citing

If this software contributed to work you are publishing, please cite it. The application itself offers
ready-made citations under **Help > How to Cite…**, carrying the exact version you ran.

```bibtex
@software{sharma2026anuprayoglinux,
  author  = {Sharma, Shilpam},
  title   = {{AnuPrayog: Tarang (Linux)}},
  version = {2.12.0.0},
  year    = {2026},
  doi     = {10.5281/zenodo.21988908},
  url     = {https://github.com/shilpam-sharma/Anuprayog-Tarang-Linux-Releases},
  note    = {Free to use, closed source. See the EULA for full terms.}
}
```

Two DOIs are available, and they answer different questions:

- **10.5281/zenodo.21988908** — the *concept* DOI. Cites this Linux
  build in general; always resolves to the newest version.
- Each release also carries its own *version* DOI, shown on that
  release's Zenodo record. If your results depend on the software's
  behaviour, cite the version DOI: it is the only identifier that says
  which build produced your numbers.

## How this differs from the Windows build

- Packaged as a single AppImage instead of an installer — no admin rights or install step needed.
- `.opj` Origin-file import uses a Linux build of the same open-source `liborigin` parser the Windows
  build uses (GPLv3; see `THIRD_PARTY_LICENSES.md`), rebuilt from the same source.
- `.trg`/`.anu` double-click file association isn't wired up yet on Linux (AppImages don't get
  installer-time hooks the way a Windows installer does) — open files from within the app for now.

## What is in this repository

This repository exists so that Linux releases are publicly reachable. It carries the AppImage, the
release notes, the licence and the third-party attributions. **The source code is not public** — it
lives in a private repository and is not distributed.
