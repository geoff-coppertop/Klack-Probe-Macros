# Klack Probe Macros

These macros are a fork of the great one implemented for the popular Voron [Klicky Probe](https://github.com/jlas1/Klicky-Probe)
The changes implemented are intended to simplify and make them compatible with Cartesian Bed Slinger that are the target of the `Klack Probe`

## Installation

The macros are currently separated by function and the `klack-probe.cfg` file include the remaining cfg files with the functionality that you want to enable, this keeps klipper's printer.cfg cleaner.

Other important files to mentions are `klack-macros.cfg` that stores all the general macros (like the dock and attach macros, this file is required on all the printers) and the `klack-variables.cfg` where it's necessary to configure a couple of printer specific information like the dock location.

The macro are expanding the standard klipper function with a attach and dock command, so that you can use all the klipper commands without the need to manually attach and dock the printer.

Here is a complete list of all the available functionality / cfg files:

* `klack-probe.cfg` (includes all the necessary files in klipper)
* `klack-variables.cfg`, stores all the Klicky variables, printer specific, should not be necessary to update very often
* `klack-bed-mesh-calibrate.cfg`, bed mesh helper scripts, assumes bed mesh is already configured, includes a commented example, further help on setup [here](https://www.klipper3d.org/Bed_Mesh.html#bed-mesh)
* `klack-adaptive-bed-mesh-calibrate.cfg`, adaptive bed mesh helper scripts, is an alternative of the provious cfg file that include the great adaptive bed mesh macro. More information about adaptive bed mesh [here](https://gist.github.com/ChipCE/95fdbd3c2f3a064397f9610f915f7d02)
* `klack-screws-tilt-calculate.cfg`, screws tilt adjust helper script, knowing where the bed screws are, it will assist in leveling the bed by calculating on the number of times each screw should be rotated, assumes that the configuration is already defined, further help on setup [here](https://www.klipper3d.org/Manual_Level.html#adjusting-bed-leveling-screws-using-the-bed-probe)

You can enable the functions that you would like to use in the `klack-probe.cfg`.