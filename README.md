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
 
