# KlipperScripts
A collection of Klipper scripts and configs that we use on our printers.

# development.cfg

Contains macros useful for devlopment of other macros and configurations.

## DUMP_PARAMETERS

The `DUMP_PARAMETERS` macro will print wach field inside the `printer` object. If the field is a map, it will also print the contents of the map.

# heatsoak.cfg

Contains macros that are useful to manage heating of the chamber.

## HEATSOAK

The `HEATSOAK` macro will heat the bed to a specified temperature (using the `TARGET=` parameter).
It will do so by raising the target in small increments above the current temperature, and skipping to the next increment when the temeperature is slightly
below the target. This ensures that the power going to the bed is maximized and the heating never times out (not heating at expected rate).
It is also possible to configure a list of fans to turn on during heating to aid with hear dispersion
