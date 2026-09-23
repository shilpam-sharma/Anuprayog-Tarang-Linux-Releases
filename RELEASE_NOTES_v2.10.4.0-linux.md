# AnuPrayog: Tarang (Linux) v2.10.4.0

Brings this Linux build up to date with the Windows v2.10.4.0 line -
the same feature set, packaged as a single AppImage. It gathers five
Windows releases (2.10.0.0 through 2.10.4.0) into one Linux build.

## New

- **Live Data reads date/time columns.** File watch, TCP, UDP and
  Watch Folder all used to force every incoming column to float, so a
  timestamp column arrived as all-NaN and never reached the dataset at
  all. Columns are now typed the same way the Import Wizard types them
  - numeric, else date/time, else text - decided once from the first
  real batch and then held. A date/time X column gets matplotlib's own
  date axis, exactly as an imported file does.
- **Plot X as iteration / point number**, in the Live Data dialog and
  inherited by Watch Folder through its per-folder template - for a
  logger whose interesting axis is "sample number", not a column.
- **Pattern Search plugin** (Plugins > Pattern Search). Select a range
  on a trace, then find every other segment shaped like it - matching
  on normalized cross-correlation, so it finds a similar *shape*
  rather than identical values - and chop each match into its own
  X/Y column pair. Matches are highlighted on the plot before anything
  is written, so you see what would be chopped first.
- **IR-FEL Imaging Pro plugin** - a matrix image viewer and processor.
- **Style works on every plot type.** The Style dialog now reaches the
  numbers that *define* a plot: histogram bins, range, density,
  cumulative, opacity, fill and edge colour; box plot outliers and
  notch; quiver scale. Previously the only way to try a different bin
  count was to delete the histogram and plot it again.
- **Append from File**, matching by position or by column name, plus
  copy/paste between the data sheet and the system clipboard.
- **Font family for annotation text.**

## Fixed

Four separate causes behind one long-running report - "the live data
plot is not surviving the save/close/open cycle" - each real, none of
them the whole story until the last:

- A live plot against a date column reopened with raw matplotlib date
  numbers on X instead of times: live traces never carried the flag
  the reload path reads to rebuild a date axis.
- A reopened **equal-aspect** graph collapsed to an empty plot. Every
  point was saved and restored correctly; the square plot box was
  sized before the pane was widened, so with wide date tick labels
  nothing was left and matplotlib shrank the axes to 57x57 px.
- A reopened **date-axis Line** was drawn ~1e14 times off to the
  right: the restore path converted a datetime64 X to float, which
  yields nanoseconds since the epoch rather than a date number.
- **Data Reader** and **Data Label** did nothing on any date-axis
  plot - a datetime64 X cannot be stacked with a float64 Y, and the
  failure was swallowed by the Qt slot, so clicks silently did
  nothing however precisely you clicked.

Also, an audit of the Style dialog across all 17 plot types found only
Line and Scatter fully working: eight types crashed on Apply, several
ignored the colour button or reopened the wrong colour, and an
untouched Apply quietly thinned every line and added markers to every
error-bar plot. All fixed.

## Getting started

```bash
chmod +x AnuPrayog_Tarang-2.10.4.0-x86_64.AppImage
./AnuPrayog_Tarang-2.10.4.0-x86_64.AppImage
```

Requires glibc 2.35+ (Ubuntu 22.04+, Debian 12+, Fedora 36+ and most
actively-supported distros as of 2026).
