# Klack Probe Macros

These macros are a fork of the great one implemented for the popular Voron [Klicky Probe](https://github.com/jlas1/Klicky-Probe)
The changes implemented are intended to simplify and make them compatible with Cartesian Bed Slinger that are the target of the `Klack Probe`

## Installation

The macros are currently separated by function, there is klack-probe.cfg that should include the remaining files, this both keeps klipper's printer.cfg cleaner and allow for backward compatibility.

The remaining files are the klack-macros.cfg that stores all the general macros (like the dock and attach macros, this file is required on all the printers), the klack-variables.cfg where it's necessary to configure a couple of printer specific information like the dock location.

The helper files work by expanding the standard klipper function with a attach and dock command, so that you can use all the klipper commands without the need to manually attach and dock the printer.

* klack-probe.cfg (includes all the necessary files in klipper)
* klack-variables.cfg, stores all the Klicky variables, printer specific, should not be necessary to update very often
* klack-bed-mesh-calibrate.cfg, bed mesh helper scripts, assumes bed mesh is already configured, includes a commented example, further help on setup [here](https://www.klipper3d.org/Bed_Mesh.html#bed-mesh)
* klack-adaptive-bed-mesh-calibrate.cfg, adaptive bed mesh helper scripts, is an alternative of the provious cfg file that include the great adaptive bed mesh macro. More information about adaptive bed mesh [here](https://gist.github.com/ChipCE/95fdbd3c2f3a064397f9610f915f7d02)
* klack-screws-tilt-calculate.cfg, screws tilt adjust helper script, knowing where the bed screws are, it will assist in leveling the bed by calculating on the number of times each screw should be rotated, assumes that the configuration is already defined, further help on setup [here](https://www.klipper3d.org/Manual_Level.html#adjusting-bed-leveling-screws-using-the-bed-probe)

You can enable the functions that you would like to use in the `klack-probe.cfg`.

## printer.cfg configuration

Download the appropriate files (or the zip containing them all and delete the ones that are not relevant) and upload it to your klipper Config folder.

```bash
cd ~/klipper_config/
wget https://raw.githubusercontent.com/jlas1/Klicky-Probe/main/Klipper_macros/Klipper_macros.zip
unzip Klipper_macros.zip
```

Check the klicky-probe.cfg, remove or comment the macros that are not required for your printer or that you do not want to implement.
Edit klicky-variables.cfg (there are printers specific recommendations on the printer configuration page) for klicky to operate properly.

There are some configurations that need to be checked, otherwise your will run into **out of range** problems, that is by design.

Open your printer.cfg file, comment out *safe_z_home* or *homing_override*, if you have them (the macros will take care of homing) and add the following line before the "Macros" Section.

`[include klicky-probe.cfg]`

It should look like this:

```ini
#####################################################################
# 	Macros
#####################################################################
[include klicky-probe.cfg]
```

You now need to configure the probe pin, that is printer specific, and the details are on your printer configuration guide.

Regarding you print start and end macros, with the helper scripts implemented, they do not need to be changed.

If however you would like to reduce the times that the toolhead attaches and docks the probe, you can use Attach_Probe_Lock that prevents the probe to be docked after an operation that normally would dock the probe.

**BEWARE that the probe may hit the bed depending on what you are doing**.

When you don't need the probe attached anymore, run Dock_Probe_Unlock to dock and unlock the probe.

## Euclid support

To support euclid side dock and undock, try these values

```python
#Attach move. final toolhead movement to attach the probe on the mount
#it's a relative move
Variable_attachmove_x:          -70
Variable_attachmove_y:            0
Variable_attachmove_z:            0

#Attach move2
Variable_attachmove2_x:          0
Variable_attachmove2_y:         40
Variable_attachmove2_z:          0

#Dock move, final toolhead movement to release the probe on the dock
#it's a relative move
Variable_dockmove_x:              0
Variable_dockmove_y:            -40
Variable_dockmove_z:              0
```

**you need to check what is the Z height of the Euclid Dock to possibly update the z moves above**
