# Klack Probe Macros

These macros are a fork of the great one implemented for the popular Voron [Klicky Probe](https://github.com/jlas1/Klicky-Probe)
The changes implemented are intended to simplify and make them compatible with Cartesian Bed Slinger that are the target of the `Klack Probe`

## Installation

The macros are currently separated by function and the `klack-settings.cfg` file include the remaining cfg files with the functionality that you want to enable, this keeps klipper's printer.cfg cleaner. The `klack-variables.cfg` also includes a few variables that are necessary to configure printer specific information like the dock location.

The macro are expanding the standard klipper function with a attach and dock command, so that you can use all the klipper commands without the need to manually attach and dock the printer.

Here is a complete list of all the available functionality / cfg files:

* `klack-settings.cfg`, stores all the Klicky variables, printer specific, should not be necessary to update very often
* `bed-mesh-calibrate.cfg`, bed mesh helper scripts, assumes bed mesh is already configured, includes a commented example, further help on setup [here](https://www.klipper3d.org/Bed_Mesh.html#bed-mesh)
* `adaptive-bed-mesh-calibrate.cfg`, adaptive bed mesh helper scripts, is an alternative of the provious cfg file that include the great adaptive bed mesh macro. More information about adaptive bed mesh [here](https://gist.github.com/ChipCE/95fdbd3c2f3a064397f9610f915f7d02)
* `screws-tilt-calculate.cfg`, screws tilt adjust helper script, knowing where the bed screws are, it will assist in leveling the bed by calculating on the number of times each screw should be rotated, assumes that the configuration is already defined, further help on setup [here](https://www.klipper3d.org/Manual_Level.html#adjusting-bed-leveling-screws-using-the-bed-probe)
* `z-tilt-adjust.cfg`, z tilt adjust helper script, knowing where the z motors are, it will assist in tramming the x-axis gantry to the bed, assumes that the configuration is already defined, further help on setup [here](https://www.klipper3d.org/Config_Reference.html#z_tilt)

You can enable the functions that you would like to use in the `klack-settings.cfg`.

The cleanest and easiest way to get started with Klack Probe Macros is to use Moonraker's Update Manager utility. This will allow you to easily install and helps to provide future updates when more features are rolled out!

1. `ssh` into your Klipper device and execute the following commands:

   ```bash
   cd

   git clone https://github.com/geoff-coppertop/Klack-Probe-Macros.git

   ln -s ~/Klack-Probe-Macros printer_data/config/Klack

   cp ~/Klack-Probe-Macros/klack-settings.cfg ~/printer_data/config/klack-settings.cfg
   ```

   **Note:**
   This will change to the home directory, clone the Klack Probe Macros repo, create a symbolic link of the repo to your printer's config folder, and create a copy of `klack-settings.cfg` in your config directory, ready to edit.

   It is also possible that with older setups of klipper or moonraker that your config path will be different. Be sure to use the correct config path for your machine when making the symbolic link, and when copying `klack-settings.cfg` to your config directory.

2. Open your `moonraker.conf` file and add this configuration:

   ```yaml
   [update_manager Klack_Probe_Macros]
   type: git_repo
   channel: dev
   path: ~/Klack-Probe-Macros
   origin: https://github.com/kyleisah/geoff-coppertop/Klack-Probe-Macros.git
   managed_services: klipper
   primary_branch: main
   ```

   **Note:**
   Whenever Moonraker configurations are changed, it must be restarted for changes to take effect. If you do not want moonraker to notify you of future updates to KAMP, feel free to skip this.

3. Depending on what features you want from Klack Probe Macros, you'll need to `[include]` some files in `klack-settings.cfg`

4. After you `[include]` the features you want, be sure to restart your firmware so those inclusions take effect. Don't forget to add `[include klack-settings.cfg]` to your `printer.cfg`!
