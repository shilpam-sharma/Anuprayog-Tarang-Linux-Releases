# AnuPrayog: Tarang (Linux) v2.12.0.0

Brings this Linux build up to date with the Windows v2.12.0.0 line -
the same feature set, packaged as a single AppImage. It gathers the
2.11.0.0 and 2.12.0.0 releases into one Linux build.

## New

- **X-Kiran, rebuilt.** The plugin previously could not actually fit
  X-ray data: every reflection got the same height and placeholder
  widths over a fixed background, and only scale, *a* and *c* were
  refined. It now does real **Le Bail and Rietveld refinement** -
  cell, zero shift, displacement, Thompson-Cox-Hastings profile terms,
  asymmetry, B_iso and March-Dollase texture, with intensities, scales
  and a Chebyshev background solved exactly each step. Plus full-sphere
  reflection enumeration with correct multiplicity and centering, CIF
  import, Ka2, R_wp/R_p/R_exp/chi2 with esds, and QPA. The XRR engine's
  two faults are fixed as well: it ignored layer thickness, and
  absorbing layers could amplify the beam.
- **THz-TDS Thin Film Analyzer** - batch extraction of optical
  constants and superfluid density, ported from a standalone tool with
  six genuine bugs fixed on the way in.
- **Goodness of fit for every fitting routine**, on one shared
  definition: R², adjusted R², SSR, RMSE, SD of fit, reduced χ²,
  AIC/AICc/BIC and standard errors - optionally written to a sheet
  alongside the parameters, remembered per fit window.
- **Stack plots** with fixed, automatic (no-overlap) or per-pair custom
  spacing. Offsets are always computed from the unshifted data, so
  re-stacking never compounds, and Unstack restores the originals
  exactly.
- **Network / proxy settings app-wide** (Tools > Network / Proxy
  Settings), with a connection test and plain-language failure
  reasons - every online feature goes through it, including the plugin
  installer's pip. See the Linux note below.
- **COD element and formula search** in X-Kiran, now actually working:
  the host was hard-coded, formulas were sent in the wrong notation
  ("TiO2" found nothing, "O2 Ti" finds 39), and result links were
  scraped with a pattern the live pages no longer use.
- Zoom Box shows a magnifying-glass cursor instead of a crosshair.

## Fixed

- **Legend entries now follow the plot order.** Any edit to the legend
  text, or to the graph, used to rearrange it, and Re-order Plots did
  not stick on a second open graph - every rebuild called a bare
  `ax.legend()`, which lists entries in insertion order. Eight further
  latent legend bugs were found and fixed in the same audit, including
  one legend entry *per bar* after any Style Apply on a bar chart.
- **Peak Deconvolution is far more robust** on noisy, narrow-peak data:
  start values are read from the data under each peak, every parameter
  is bounded and scaled, there is an optional background term and a
  multi-start strategy, and Auto Find Peaks works on a smoothed trace
  with a noise-aware prominence.

## Packaging

This build adds matplotlib's **SVG, EPS and PDF backends**. `savefig`
imports a backend by name at save time, so the packager never saw them
and vector export silently failed in the packaged app while working
from source - Export Graph, Batch Export, X-Kiran and IR-FEL were all
affected. `gemmi` and `periodictable` are now bundled too, for the
rebuilt X-Kiran.

## A note for Linux users

The proxy **password** is not saved on Linux. On Windows it is
encrypted with DPAPI, which has no Linux equivalent here, and writing
it to disk in plain text instead would be worse than asking for it
again. Every other proxy setting is saved normally.

## Getting started

```bash
chmod +x AnuPrayog_Tarang-2.12.0.0-x86_64.AppImage
./AnuPrayog_Tarang-2.12.0.0-x86_64.AppImage
```

Requires glibc 2.35+ (Ubuntu 22.04+, Debian 12+, Fedora 36+ and most
actively-supported distros as of 2026).
