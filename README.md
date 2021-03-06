# Preface
This document guides you through the steps for setting up the software side of things on the Sutter MOM system.

# Computer system
The current imaging control computer has an inadequate heatsink. To maximize stability, do the following:
1. CPU/system fans speed always 100%
1. Turn off intel C states
1. Disable turbo boost
1. Undervolt processor to 1.025
1. Overclock to 3.6 (ratio)

### Requirements:
* MATLAB (look for version compatible with latest scanimage)
* NI DAQmx and FlexRIO drivers (find compatible versions on scanimage website)
* The usb-to-serial adapter is a fake and won't work with official drivers. Get an older driver from http://wp.brodzinski.net/hardware/fake-pl2303-how-to-install
* A RAID array for data acquisition (optional)

# Configuration
Once everything is installed, fire up `scanimage` in MATLAB and follow the setup wizard.

## General Settings
This is where you can add your custom scripts/plugins (such as the online registration and alignment from the Janelia group). Keep default values (15 um/deg scan angle).

## Shutters
Shutters for Laser 1 and Laser 2 are separately controlled by PFI12 on DAQ 5 and DAQ 4 respectively (wired to USER2).

## Power modulation
Pockel cells for Laser 1 and Laser 2 are controlled by AO0 and AO1 on DAQ 6 respectively.

## Scanners
Scanner currently in Res/Galvo configuration. Set aux box to DAQ 5. All settings can remain as default. For Galvo, only the Y axis needs to be set. Angular range, volts per degree and park degree are 15, 1 and -8 respectively. Angular range for resonant is 15. Default setting for everything else. Don't forget that the PMTs are inverted.

## Motor Stage
Choose Sutter MP-285 from the list of devices and invert the Z axis.

## Piezo Stage
We're working with a nPFocus400 piezo stage with a range of 400 um, coupled with an LC400 Controller. Connect the command input and sensor output to the analogue BNC ports on DAQ 4. Set min/max command voltages to -10 to 10 and the range to -200 to 200 um. Plug the controller via USB to the computer and install the drivers provided on CD. To get the COM port, virtual serial communications need to be enabled first. In device manager, right click on "properties" on "USB Serial Converter" under "Universal Serial Bus controllers". Under the Advanced tab, enable "Load VCP". Unplug, wait couple seconds, plug back in. You should see a new COM port.

The stage was factory calibrated. However, recalibration is advised for maximum performance with the objective and tilt angle. This can be done with the provided software. Might need to go back-and-forth a couple times between ScanImage and nPControl to optimize the settings.
