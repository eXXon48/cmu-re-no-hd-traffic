# No HD Radio traffic

`cmu-re-no-hd-traffic` · Revised Store package · Mazda CMU150, firmware 74.00.324A

MMUI no longer loads the HD Radio traffic-image screen module (hdtrafficimage), which is US-only.

## Why

The HD Radio traffic-image screen is a US-only feature. MMUI loads its module one by one with all the others before it answers the GUI.

## What it changes

| File | How | Why |
|---|---|---|
| `/jci/mmui/mmui_config.xml` | xml-node | MMUI no longer loads the screen module(s) of this service, which it loads one by one before it answers the GUI |

`xml-node` edits address single nodes by XPath; `3way` edits are small diffs against the stock file. The Store merges them with every other installed package, refuses a real clash, and takes them back out on uninstall. No stock file is replaced as a whole.

## Install and uninstall

Install from the Revised Store app on the unit, then restart. Uninstall the same way: after the restart the unit behaves as stock again.

Safety: every change is recorded in the Store's vanilla index, so the boot-loop tripwire reverts it on its own if the unit fails to boot several times in a row. No package edits the boot script above the tripwire line.

## Requires

- `cmu-re-store (>= 0.13.4)`

## Part of

- `cmu-re-speedup-boot-max`

## Develop

```sh
sh test/run.sh                                  # manifest and payload checks
sh tools/mkpkg.sh <version> <rvp-pack> out.rvp   # build the .rvp
```

Releases: a `dev/vN` tag on `develop` gives a dev prerelease, a `vN` tag on `main` a release; CI packs the `.rvp` and attaches it to the GitHub release.
