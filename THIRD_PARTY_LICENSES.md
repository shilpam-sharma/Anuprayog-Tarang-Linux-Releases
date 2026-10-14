# Third-Party Licenses

AnuPrayog: Tarang is built on and distributes a number of third-party
open-source components. This file lists every component bundled into the
packaged application (the Nuitka-built binary and the AppImage), its
license, and its copyright notice. Full license text for each license
type is kept in the [`licenses/`](licenses/) folder of this repository and
linked below.

This inventory mirrors the Windows build's own third-party license file
(see the [Windows releases repo](https://github.com/shilpam-sharma/Anuprayog-Tarang-Releases)),
adjusted for what's actually bundled on Linux: Windows-only components
(`pywin32`) are dropped, and the Linux AppImage additionally bundles a
set of standard Linux system libraries (Qt's xcb platform-plugin runtime
dependencies, GLib/D-Bus, ICU, etc.) that the AppImage packaging step
(`linuxdeploy`) pulls in from the build system's own package repositories
— see "Linux system libraries" below.

## A note on Qt / PySide6 (LGPL-3.0)

PySide6 (Qt for Python) and its `shiboken6` binding-generator runtime are
licensed under the user's choice of **LGPL-3.0-only, GPL-2.0-only, or
GPL-3.0-only**; this application uses the **LGPL-3.0** option. Qt itself
is under the same terms.

The build ships Qt/PySide6/shiboken6 as **separate shared library files**
alongside the main executable (dynamic linking), not statically linked
into the executable itself. This is what LGPL-3.0 requires for a
proprietary application to link against it without the application
itself being subject to LGPL/GPL terms: the libraries can be inspected,
and a technically capable user can replace them with a modified or newer
LGPL-compatible build of Qt/PySide6/shiboken6, per LGPL-3.0 §4(d)(1)
("a suitable shared library mechanism"). The full LGPL-3.0 text (which
incorporates GPL-3.0 by reference for the terms it doesn't override) is
included as [`licenses/LGPL-3.0.txt`](licenses/LGPL-3.0.txt) and
[`licenses/GPL-3.0.txt`](licenses/GPL-3.0.txt). Qt's own source code is
publicly available from The Qt Company at <https://www.qt.io/download-open-source>
and PySide6's source from <https://code.qt.io/cgit/pyside/pyside-setup.git/>.

**`cvxopt` (GPLv3) is deliberately excluded from the build** via Nuitka's
`--nofollow-import-to=cvxopt` — it is an optional solver dependency of
`statsmodels` that this application never calls, and shipping GPLv3 code
unnecessarily was avoided rather than accepted.

**`liborigin` (GPLv3)** — the `.opj` Origin-file import backend — is
**not linked into the application's own process** on Linux either: it
runs as a separate subprocess, communicating only through a JSON file on
disk, the same arm's-length relationship a proprietary app has with any
external GPL CLI tool it shells out to. Its full source is included in
this application under GPLv3 §6 (see the source repository's
`origin_import_helper/liborigin_src/`, including `COPYING`).

## Bundled components

| Component | Version | License | Copyright | License text |
|---|---|---|---|---|
| NumPy | 2.1.3 | BSD-3-Clause | Copyright (c) 2005-2024, NumPy Developers | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| pandas | 2.2.3 | BSD-3-Clause | Copyright (c) 2008-2011 AQR Capital Management, LLC, Lambda Foundry, Inc. and PyData Development Team; (c) 2011-2023 Open source contributors | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| SciPy | 1.15.1 | BSD-3-Clause | Copyright (c) 2001-2002 Enthought, Inc.; 2003-2024 SciPy Developers | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| Matplotlib | 3.10.0 | Matplotlib License (PSF-derived) | Copyright (c) 2012- Matplotlib Development Team; (c) 2002-2011 John D. Hunter | [matplotlib-license](licenses/matplotlib-license.txt) |
| PySide6 (Qt for Python) | 6.11.1 | LGPL-3.0-only | Copyright (c) The Qt Company Ltd. | [LGPL-3.0](licenses/LGPL-3.0.txt) / [GPL-3.0](licenses/GPL-3.0.txt) |
| shiboken6 | 6.11.1 | LGPL-3.0-only | Copyright (c) The Qt Company Ltd. | [LGPL-3.0](licenses/LGPL-3.0.txt) / [GPL-3.0](licenses/GPL-3.0.txt) |
| Qt6 (Core/Gui/Widgets/Network/OpenGL/Svg/Pdf/DBus/PrintSupport/WaylandClient) | 6.x | LGPL-3.0-only | Copyright (c) The Qt Company Ltd. | [LGPL-3.0](licenses/LGPL-3.0.txt) / [GPL-3.0](licenses/GPL-3.0.txt) |
| statsmodels | 0.14.4 | BSD-3-Clause | Copyright (c) statsmodels Developers | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| PyWavelets | 1.8.0 | MIT | Copyright (c) 2006-2012 Filip Wasilewski; (c) 2012-2020 The PyWavelets Developers | [MIT](licenses/MIT.txt) |
| certifi | 2024.6.2 | MPL-2.0 | Copyright (c) Kenneth Reitz and certifi contributors | [MPL-2.0](licenses/MPL-2.0.txt) |
| charset-normalizer | 3.4.0 | MIT | Copyright (c) Ahmed TAHRI | [MIT](licenses/MIT.txt) |
| trio | 0.28.0 | MIT (dual MIT/Apache-2.0) | Copyright (c) 2017 Nathaniel J. Smith and other contributors | [MIT](licenses/MIT.txt) |
| zstandard | 0.23.0 | BSD-3-Clause | Copyright (c) Gregory Szorc | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| msgpack | 1.1.0 | Apache-2.0 | Copyright (C) 2008-2011 INADA Naoki | [Apache-2.0](licenses/Apache-2.0.txt) |
| pytz | 2024.1 | MIT | Copyright (c) Stuart Bishop | [MIT](licenses/MIT.txt) |
| python-dateutil | 2.8.2 | BSD-3-Clause (dual BSD/Apache-2.0) | Copyright (c) 2003-2011 Gustavo Niemeyer; (c) 2012-2014 dateutil contributors | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| packaging | 24.2 | Apache-2.0 (dual Apache-2.0/BSD-2-Clause) | Copyright (c) Donald Stufft and individual contributors | [Apache-2.0](licenses/Apache-2.0.txt) |
| pyparsing | 3.2.1 | MIT | Copyright (c) 2003-2024 Paul T. McGuire | [MIT](licenses/MIT.txt) |
| kiwisolver | 1.4.8 | BSD-3-Clause | Copyright (c) 2013-2024, Nucleic Development Team | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| cycler | 0.12.1 | BSD-3-Clause | Copyright (c) 2015, matplotlib project | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| fonttools | 4.55.3 | MIT | Copyright (c) Just van Rossum | [MIT](licenses/MIT.txt) |
| Pillow | 11.1.0 | MIT-CMU | Copyright (c) 2010 by Jeffrey A. Clark and contributors; historically (c) 1997-2011 Secret Labs AB, Fredrik Lundh | [MIT-CMU](licenses/MIT-CMU.txt) |
| ContourPy | 1.3.1 | BSD-3-Clause | Copyright (c) 2021-2024, ContourPy Developers | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| patsy | 0.5.6 | BSD-2-Clause | Copyright (c) 2011-2016, Patsy Developers | [BSD-2-Clause](licenses/BSD-2-Clause.txt) |
| six | 1.16.0 | MIT | Copyright (c) 2010-2020 Benjamin Peterson | [MIT](licenses/MIT.txt) |
| pyarrow (Apache Arrow) | 19.0.0 | Apache-2.0 | Copyright (c) The Apache Software Foundation | [Apache-2.0](licenses/Apache-2.0.txt) |
| lxml | 5.3.0 | BSD-3-Clause | Copyright (c) 2004 Infrae | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| greenlet | 3.5.2 | MIT | Copyright (c) Armin Rigo, Christian Tismer and contributors | [MIT](licenses/MIT.txt) |
| MarkupSafe | 3.0.2 | BSD-3-Clause | Copyright (c) 2010 Pallets | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| jaraco.classes | 3.4.0 | MIT | Copyright (c) Jason R. Coombs | [MIT](licenses/MIT.txt) |
| jaraco.functools | 4.1.0 | MIT | Copyright (c) Jason R. Coombs | [MIT](licenses/MIT.txt) |
| jaraco.context | 6.0.1 | MIT | Copyright (c) Jason R. Coombs | [MIT](licenses/MIT.txt) |
| OpenBLAS (bundled inside NumPy/SciPy's own shared libraries) | (per NumPy/SciPy wheel) | BSD-3-Clause | Copyright (c) 2011-2014, The OpenBLAS Project | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| Python runtime | 3.12 | PSF-2.0 | Copyright (c) Python Software Foundation | [PSF-2.0](licenses/PSF-2.0.txt) |
| Nuitka (compiler/runtime bootstrap code embedded in the build) | 4.1.3 | Apache-2.0 | Copyright (c) Kay Hayen | [Apache-2.0](licenses/Apache-2.0.txt) |
| PyQtGraph | 0.13.7 | MIT | Copyright (c) 2012 Luke Campagnola | [MIT](licenses/MIT.txt) |
| PyOpenGL | 3.1.10 | BSD-style (PyOpenGL license) | Copyright (c) 2005-2009, Michael C. Fletcher and Contributors | [PyOpenGL-license](licenses/PyOpenGL-license.txt) |
| PyOpenGL-accelerate | 3.1.10 | BSD-style (OpenGL-ctypes PyOpenGL-accelerate License) | Copyright (c) 2005-2009, Michael C. Fletcher and Contributors | [PyOpenGL-license](licenses/PyOpenGL-license.txt) |
| scikit-rf | 2.1.0 | BSD-3-Clause | Copyright (c) scikit-rf Development Team | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| astropy | 8.0.1 | BSD-3-Clause | Copyright (c) 2011-2026, Astropy Developers | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| h5py | 3.16.0 | BSD-3-Clause | Copyright (c) 2008 Andrew Collette and contributors | [BSD-3-Clause](licenses/BSD-3-Clause.txt) |
| gemmi | 0.7.5 | MPL-2.0 | Copyright (c) Global Phasing Ltd.; Marcin Wojdyr | [MPL-2.0](licenses/MPL-2.0.txt) |
| periodictable | 2.1.0 | Public domain | Paul Kienzle and contributors (NIST); see the package's own LICENSE.txt | (public domain - no licence text required) |

## Linux system libraries

The AppImage additionally bundles a standard set of Linux system shared
libraries so it runs without requiring them to be pre-installed on the
target system — Qt's xcb-platform-plugin runtime dependencies
(`libxcb-cursor`, `libxcb-icccm`, `libxcb-image`, `libxcb-keysyms`,
`libxcb-randr`, `libxcb-render-util`, `libxcb-shape`, `libxcb-sync`,
`libxcb-xfixes`, `libxcb-xkb`, `libxkbcommon`, `libxkbcommon-x11`),
GLib/GObject/GIO, D-Bus, ICU, libpng, brotli, and similar. These are
standard components of any Linux desktop and are licensed under
permissive or LGPL terms (MIT, BSD, LGPL-2.1+) by their respective
upstream projects (freedesktop.org, GNOME, ICU-TC, etc.), not authored by
or specific to this application. They were built from the Ubuntu 22.04
package archive as part of the AppImage packaging step and are not
modified.

## Where these come from

This list reflects the Windows build's own `THIRD_PARTY_LICENSES.md`
(regenerated by inspecting `build\main.dist\`'s actual contents and each
package's installed metadata), adjusted for the Linux build's actual
bundled component set as described above.
