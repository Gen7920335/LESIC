# LESIC

**Lowtemp Extrusion Support Interface Calibration**

LESIC is a standalone G-code generator for calibrating low-temperature support interface behavior in FDM 3D printing. It creates a circular calibration pattern with controlled MVS progression and stepwise temperature changes, making it easier to compare how support interface layers behave under different low-temperature extrusion conditions.

**Web app:** [https://gen7920335.github.io/LESIC/](https://gen7920335.github.io/LESIC/)

## What Is Lowtemp Extrusion Support Interface?

Lowtemp Extrusion Support Interface means printing the support-contact interface at a lower nozzle temperature than the main part. The goal is to reduce bonding strength between support and model so supports separate more cleanly, while still keeping acceptable underside surface quality.

Even when the model and the support are printed with the same material, this approach can be used to fine-tune interface adhesion so the support still separates cleanly without making the supported surface excessively rough.

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

## Supported Nozzle Sizes

The web UI currently supports these nozzle sizes, with automatic circular line width selection:

- `0.8 mm` -> `0.96 mm`
- `0.6 mm` -> `0.72 mm`
- `0.4 mm` -> `0.48 mm`
- `0.25 mm` -> `0.30 mm`
- `0.2 mm` -> `0.24 mm`
- `0.15 mm` -> `0.18 mm`

## How to Use

LESIC generates a circular calibration print for checking how a filament behaves at different extrusion temperatures and volumetric flow rates.

Set the minimum and maximum MVS values, then set the highest and lowest extrusion temperatures you want to test. The print starts at the front of the circular toolpath using the minimum MVS. Within each layer, the MVS gradually increases as the nozzle moves around the circle. By the time the toolpath returns to the front starting point, it has reached the maximum MVS. The next layer then starts again from the front.

The nozzle temperature starts from the highest extrusion temperature. After the configured number of layers, the temperature drops by the configured temperature step. The default setting is:

```text
Drop 1°C every 10 layers
```

After the print is complete, inspect where the circular wall starts to fail, under-extrude, break apart, or become visibly unstable. That failure point shows the practical limit of the filament at that temperature and MVS.

In general, lower nozzle temperatures reduce the usable MVS. If you want a support interface that prints as slowly and weakly as possible, choose a temperature where the filament still extrudes at the front starting point of the circle. If you want a more stable support interface that still separates more easily than normal printing temperatures, choose a temperature where the tower remains stable at around 8 mm³/s or higher.

A practical workflow is:

1. Generate and print the LESIC calibration G-code.
2. Find the lowest temperature where extrusion still starts reliably.
3. Check which temperatures remain stable at your target MVS.
4. Create a separate virtual filament profile in your slicer for support-interface use.
5. Enter the selected extrusion temperature and maximum volumetric speed into that filament profile.
6. Use that virtual filament profile only for the support interface.

For example, if the print barely extrudes at 185°C but becomes stable from 195°C at 8 mm³/s, use 185°C only for very slow and weak interface printing. Use around 195°C or higher if you want a more reliable interface that still separates more easily than normal-temperature support material.


## Intended Use

LESIC is meant for users who want to tune support interface removal and supported-surface finish by testing lower interface temperatures in a controlled, repeatable print.

## Recommended Print Conditions

For best comparison results, keep the surrounding support settings as consistent as possible. In OrcaSlicer, use the matching support-interface settings below:

- `Support expansion`: `1 mm` or more
- `Fan speed / Cooling`: keep at `100%`
- `Top interface spacing`: `0`
- `Top interface pattern`: `Rectilinear Interlaced`
- `Top interface pattern angle`: `22.5`
- `Top interface layers`: `4`

## Real Print Examples

These photos show example output and supported-surface results from actual printed samples.

![Example print 1](docs/images/example_print_1.jpg)

![Example print 2](docs/images/example_print_2.jpg)

![Example print 3](docs/images/example_print_3.jpg)
