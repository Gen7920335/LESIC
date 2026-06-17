# LESIC

**Lowtemp Extrusion Support Interface Calibration**

LESIC is a standalone G-code generator for calibrating low-temperature support interface behavior in FDM 3D printing. It creates a circular calibration pattern with controlled MVS progression and stepwise temperature changes, making it easier to compare how support interface layers behave under different low-temperature extrusion conditions.

**Web app:** [https://gen7920335.github.io/LESIC/](https://gen7920335.github.io/LESIC/)

## What Is Lowtemp Extrusion Support Interface?

Lowtemp Extrusion Support Interface means printing the support-contact interface at a lower nozzle temperature than the main part. The goal is to reduce bonding strength between support and model so supports separate more cleanly, while still keeping acceptable underside surface quality.

## What LESIC Does

- Generates standalone calibration G-code
- Sweeps MVS across a circular toolpath
- Steps temperature across multiple bands
- Adds a printable identification label under the model
- Lets you preview the calibration layout in the browser before export

## Current Web UI Defaults

- `mvs_min`: `8`
- `mvs_max`: `24`
- default nozzle: `0.4 mm`
- circular line width: automatically selected from nozzle size
- bottom label layout: fixed `three-line`

## Supported Nozzle Sizes

The web UI currently supports these nozzle sizes, with automatic circular line width selection:

- `0.8 mm` -> `0.96 mm`
- `0.6 mm` -> `0.72 mm`
- `0.4 mm` -> `0.48 mm`
- `0.25 mm` -> `0.30 mm`
- `0.2 mm` -> `0.24 mm`
- `0.15 mm` -> `0.18 mm`

## Intended Use

LESIC is meant for users who want to tune support interface removal and supported-surface finish by testing lower interface temperatures in a controlled, repeatable print.
