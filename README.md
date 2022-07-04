# klipper_config
This repo contains generic and printer-specific Klipper configuration for my printers. 

## How it works 

printer.cfg should never be checked into the repo. Instead, your printer.cfg should include
a single file with some name associated with that printer. That printer-specific file can then
define any printer-specific configuration, like for example the USB ID, and include additional 
files for:
- Configuration files specific to that printer model
- Configuration file specific to hardware that printer contains (for example, the pin definitions for a specific controller board)
- Generic macros
- Printer or printer model specific macros

## Directory Structure

The example below shows a directory structure for a Voron v0 printer named "ppe".

```
printer.cfg (not checked in)
-> ppe.cfg
  -> mcu-boards/skr-mini-e3-v2.cfg
  -> voron-v0/voron-v0.cfg
  -> voron-v0/macros.cfg
  -> macros/macros.cfg
```