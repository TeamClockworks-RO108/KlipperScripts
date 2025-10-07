# KlipperScripts
A collection of Klipper scripts and configs that we use on our printers.

# DUMP_PARAMETERS (development.cfg)

The `DUMP_PARAMETERS` macro will print wach field inside the `printer` object. If the field is a map, it will also print the contents of the map.

# HEATSOAK (heatsoak.cfg)

The `HEATSOAK` macro will heat the bed to a specified temperature (using the `TARGET=` parameter).
It will do so by raising the target in small increments above the current temperature, and skipping to the next increment when the temeperature is slightly
below the target. This ensures that the power going to the bed is maximized and the heating never times out (not heating at expected rate).
It is also possible to configure a list of fans to turn on during heating to aid with hear dispersion.

TODO: turn off the fans after the heatsoak.

# PRINT_START (print_lifecycle.cfg)

The `PRINT_START` does quite a few things:
 * Checks that the slicer profile version supplied (in the `VERSION=` parameter) is an accepted value.
 * Overheat the bed by a few degrees (using the `HEATSOAK` macro) and blow the fans to disperse the chamber heat.
 * Wait for the bed to cool down to required temperature.
 * Run the homing, quad gantry level and meshing procedures.
 * Print a pruge line containing a straight section and a zigzag section that aids in seeing how the bed adhesion will be on the print.
 * Load the initial tool, if ERCF is configured

Example complete start G-code in PrusaSlicer:
```gcode
PRINT_START EXTRUDER={first_layer_temperature[initial_tool]} BED=[first_layer_bed_temperature] TOTAL_LAYER={total_layer_count} VERSION=2
``` 

For ERCF printers, the start G-code will look like this:
```gcode
MMU_START_SETUP INITIAL_TOOL={initial_tool} REFERENCED_TOOLS=!referenced_tools! TOOL_COLORS=!colors! TOOL_TEMPS=!temperatures! TOOL_MATERIALS=!materials! FILAMENT_NAMES=!filament_names! PURGE_VOLUMES=!purge_volumes!
PRINT_START EXTRUDER={first_layer_temperature[initial_tool]} BED=[first_layer_bed_temperature] TOTAL_LAYER={total_layer_count} VERSION=2 ACTION=heat_calibrate
MMU_START_CHECK
MMU_START_LOAD_INITIAL_TOOL
PRINT_START EXTRUDER={first_layer_temperature[initial_tool]} BED=[first_layer_bed_temperature] TOTAL_LAYER={total_layer_count} VERSION=2 ACTION=purge
```
