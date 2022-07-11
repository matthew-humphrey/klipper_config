# klipper_config
This repo contains generic and printer-specific Klipper configuration for my printers. 

## How it works 

This repo uses an approach to make Klipper configuration composable from a number of reusable config files.
I prefer this approach over the monolithic configuration file because it allows me to minimize the amount
of effort to configure and maintain multiple printers and multiple types of printers.

This approach also facilitates using git/GitHub to version and back-up 3D printer configuration.

For this approach to work, Klipper's printer.cfg file must obey the following rules:
- It should be just a shell that includes some other file that contains the actual printer configuration. This allows Klipper to write back to the file without overwriting the versioned configuration file.
- printer.cfg should not be checked into git, and should instead be added to .gitignore

The printer-specific configuration file included by printer.cfg can then include various other files as needed to "mix in"
configuration and macros appropriate for that printer. This file can also set certain configuration properties that allow
a generic (printer independent) set of macros to work correctly for that printer.

## Example Configuration

The example below shows a directory structure for a Voron v0 printer named "ppe". 

```
# Not checked in added to .gitignore
printer.cfg 

  # Physical printer definition. This file is directly included by printer.cfg
  # In addition to including the files below, this file should define the variables
  # in the _MACRO_CONFIG macro.
-> ppe.cfg 

    # Includes files to define kinematics and reasonable defaults for the Voron V0/V0.1 printer
  -> printers/voron-v0.cfg 

    # Configuration for the mini-afterburner extruder
  -> extruders/mini-ab.cfg 

    # Configuration for the Phaetus Dragonfly BMO hotend
  -> hotends/dragonfly-0.4.cfg 

    # Configuration for the small OLED v0Display and click-wheel
  -> displays/v0-display.cfg  

    # Top-level macro file that includes numerous files that define the actual macros
  -> macros/macros.cfg
```

## Attribution

The approach of composable configuration is one I learned from Discord user Pinky#1302 and his [Klipper config github repo](Pinky#1302). 
Since that time, I also purchased and built a RatRig V-Core3 kit, and learned about the wonderful klipper configuration that is part
of the RatOS project used with those printers. Many of the macros here are borrowed directly from RatOS.