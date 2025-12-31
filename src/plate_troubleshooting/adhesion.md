# Adhesion

## Clean. Your. Plate.

Warping and adhesion are caused by your plate not being clean 90% of the time.

Your build plate depends on interesting interactions of heat and chemistry to bond your filament while printing, but let it go when cooled. None of that works if your build plate is covered in contaminants.

The most common contaminants are oils from your hands, contamination from other prints, and other contaminants from the environment. Open printers like the A1 are especially prone to environmental contamination.

Before you do anything else, deep-clean your plate.

> [!CAUTION]
> Do not use IPA or soap on the LUX plates.

1. Remove the plate from the printer.
2. Clean the plate according to the plate's [cleaning instructions](https://darkmoon3d.com/pages/plate-comparison) (generally Dawn/Fairy dish soap, hot water, and a clean nylon scrubber or sponge).
3. Let the plate dry completely, or dry it with a lint-free paper towel.
4. Do not touch the plate with your bare hands.
5. Reinstall the plate on the printer.

Try your print again. If it's still not good, try the following steps.

## Bed Leveling & Z-Offset

Getting the right Z-offset and bed leveling is key to a good first layer.

Here's how to make sure you get a good one.

### Reset the bed mesh

On Bambu printers, there's an issue that sometimes causes the bed mesh to be incorrect, especially if you're using a different plate than you originally calibrated with.

1. Power off your printer for at least 30 seconds.
2. Power on your printer.
3. Make sure your Darkmoon plate is properly placed on the bed.
4. Run your printer's bed leveling calibrations
   1. on H2/P2, do both the normal and high-temp bed leveling calibrations.

Try your print again. This solves about 50% of issues we see in discord.

### Z-Offset

#### Plate Settings

If you find that your first layers are just a little far from the plate, Try using the "Textured PEI" setting if you were using the "Smooth PEI" plate setting. The "Textured PEI" plate setting puts the nozzle a bit closer to the plate, and is often enough to fix a z-offset not close enough issue.

#### Manual Z-Offset

If the plate settings don't work, you can manually adjust the z-offset in the filament settings.

![Filament Settings G-Code](filament_settings_gcode.png)

Edit the Filament Start G-Code to add a Z-offset adjustment. This gcode will add a small amount of lift to the nozzle. You'll want to tune this in very small steps.

Add this after the `; filament start gcode` comment in the start G-code text box.

```gcode
;===== Z-offset adjustment for Smooth PEI Plate =====
{if curr_bed_type=="High Temp Plate"}
G29.1 Z{0.01} ; Lift nozzle slightly
{endif}
```

The important part is the `G29.1 Z{0.01}` line. Positive values move the nozzle away from the plate, negative values move it closer.
