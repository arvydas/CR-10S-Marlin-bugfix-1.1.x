# Marlin 3D Printer Firmware for Creality CR-10S 500

This is a bugfix release branch source code for 1.1.7 downloaded on the 2017-12-15. This may be updated along the way.

I take no responsibility to damage to your 3D printer or your body parts when using this guide. Be smart.

This source contains configuration for my Creality CR-10S 500mm 3D printer.

## Prerequisites

- BLTouch sensor (or clone)
- CR-10S with unlocked bootloader
- This source code

## Configure for your 3D printer

You will need to adjust the following parameters in Configuration.h:

- X_BED_SIZE, Y_BED_SIZE, Z_MAX_POS - the size of the printing cube. I think CR-10S comes in 300, 400 and 500mm sizes

## Print the BLTouch holder

I am using this mount https://www.thingiverse.com/thing:2493610

It is not perfect is it is hard to tighten all screws, because mount is either in the way or BLTouch is covering the screws, but it is working for now.

Few tips:

- Mount can be printed in PLA
- Make sure you tighten screws!

## Wire BLTouch

<img align="top" width=175 src="buildroot/share/pixmaps/cr-10s/main-board.png" />

BLTouch consists of 2 connectors:

- 3 Pin connector works as servo
- 2 Pin connector works as endstop

My board is green. There is a 3x4 pin connector on the board next to Ext1 and Ext2 connectors. You need to use D11 labeled pins and connect BLTouch like this:

         D11 <-> BLTouch
         -------------
          5V <-> Red
          G  <-> Brown 
    unlabled <-> Orange

You have to replace the Z-min endstop switch with BLTouch 2 pin connector. The easiest way to do this I found by removing the connector next to Z-Min endstop and plugging BLTouch to the same connector.

## How to use

- Compile and upload firmware
- Test deploy and stow of BLTouch using menus in LCD
- Lift Z to about 40mm
- Home all axis using Prepare section in the menu
- Use your finger to push the pin back to test that BLTouch detection works before Z reaches the bed. Z should go back up and deploy sensor again. Use your finger to push the pin again.
- If printer stops, this means that the sensor works and now you can do the home axis and this time use the sensor to touch the bed 

Stay next to power switch to turn off the machine in case nozzle rams into the bed if sensor is misconfigured or malfunctioned.

Will update this section along the way. I am currently focussed on making sure that repeatability is within margins for the sensor.

## Using Unified Bed Leveling (UBL)

There are menu items available for UBL now. I will update this section later. For now use G-code to do bed leveling.

- Level build plate on the four corners, you will find a menu item for this
- Start by running G29 P1 command. Your printer will probe many points on your bed to create a mesh. This may take a while!
- When probing finishes, run G29 S to save the mesh
- Activate mesh with G29 A command
- Save settings with M500

Now it is time to adjust the distance between the BLTouch sensor and your hot end tip. By default the Z offset available in the main menu -> Prepare -> Motion section is set to 0.000mm. You will need to adjust this safely. Start a very basic print (a cube) on the center of the build plate and watch the first layer. If the extruder does not reach the build plate, set the value of the Z offset to -0.2mm and start printing again. You will need to clean the nozzle after each attempt! Keep decreasing the offset until you get a nice adhesion for the first layer. In my case the value for the Z offset was -0.76mm

More details about bed leveling can be found here:

http://marlinfw.org/docs/features/unified_bed_leveling.html

## Support

I have very limited time to provide support, but you can either have your questions asked in the issue tracker for this repository or CR-10S Facebook group https://www.facebook.com/groups/1408301692623865/

## Below information from the original Marlin firmware readme

<img align="right" src="../../raw/1.1.x/buildroot/share/pixmaps/logo/marlin-250.png" />

## Marlin 1.1

Marlin 1.1 represents an evolutionary leap over Marlin 1.0.2. It is the result of over two years of effort by several volunteers around the world who have paid meticulous and sometimes obsessive attention to every detail. For this release we focused on code quality, performance, stability, and overall user experience. Several new features have also been added, many of which require no extra hardware.

For complete Marlin documentation click over to the [Marlin Homepage <marlinfw.org>](http://marlinfw.org/), where you will find in-depth articles, how-to videos, and tutorials on every aspect of Marlin, as the site develops. For release notes, see the [Releases](https://github.com/MarlinFirmware/Marlin/releases) page.

## Stable Release Branch

This Release branch contains the latest tagged version of Marlin (currently 1.1.8 – December 2017).

Previous releases of Marlin include [1.0.2-2](https://github.com/MarlinFirmware/Marlin/tree/1.0.2-2) (December 2016) and [1.0.1](https://github.com/MarlinFirmware/Marlin/tree/1.0.1) (December 2014). Any version of Marlin prior to 1.0.1 (when we started tagging versions) can be collectively referred to as Marlin 1.0.0.

## Contributing to Marlin

Click on the [Issue Queue](https://github.com/MarlinFirmware/Marlin/issues) and [Pull Requests](https://github.com/MarlinFirmware/Marlin/pulls) links above at any time to see what we're currently working on.

To submit patches and new features for Marlin 1.1 check out the [bugfix-1.1.x](https://github.com/MarlinFirmware/Marlin/tree/bugfix-1.1.x) branch, add your commits, and submit a Pull Request back to the `bugfix-1.1.x` branch. Periodically that branch will form the basis for the next minor release.

Note that our "bugfix" branch will always contain the latest patches to the current release version. These patches may not be widely tested. As always, when using "nightly" builds of Marlin, proceed with full caution.

## Current Status: In Development

Marlin development has reached an important milestone with its first stable release in over 2 years. During this period we focused on cleaning up the code and making it more modern, consistent, readable, and sensible.

## Future Development

Marlin 1.1 is the last "flat" version of Marlin!

Arduino IDE now has support for folder hierarchies, so Marlin 1.2 will have a [hierarchical file structure](https://github.com/MarlinFirmware/Marlin/tree/breakup-marlin-idea). Marlin's newly reorganized code will be easier to work with and form a stronger starting-point as we get into [32-bit CPU support](https://github.com/MarlinFirmware/Marlin/tree/32-Bit-RCBugFix-new) and the Hardware Access Layer (HAL).

[![Coverity Scan Build Status](https://scan.coverity.com/projects/2224/badge.svg)](https://scan.coverity.com/projects/2224)
[![Travis Build Status](https://travis-ci.org/MarlinFirmware/Marlin.svg)](https://travis-ci.org/MarlinFirmware/Marlin)

## Marlin Resources

- [Marlin Home Page](http://marlinfw.org/) - The Marlin Documentation Project. Join us!
- [RepRap.org Wiki Page](http://reprap.org/wiki/Marlin) - An overview of Marlin and its role in RepRap.
- [Marlin Firmware Forum](http://forums.reprap.org/list.php?415) - Find help with configuration, get up and running.
- [@MarlinFirmware](https://twitter.com/MarlinFirmware) on Twitter - Follow for news, release alerts, and tips & tricks. (Maintained by [@thinkyhead](https://github.com/thinkyhead).)

## Credits

The current Marlin dev team consists of:
 - Roxanne Neufeld [[@Roxy-3D](https://github.com/Roxy-3D)]
 - Scott Lahteine [[@thinkyhead](https://github.com/thinkyhead)]
 - Bob Kuhn [[@Bob-the-Kuhn](https://github.com/Bob-the-Kuhn)]

Notable contributors include:
 - Alberto Cotronei [[@MagoKimbra](https://github.com/MagoKimbra)]
 - Andreas Hardtung [[@AnHardt](https://github.com/AnHardt)]
 - Bernhard Kubicek [[@bkubicek](https://github.com/bkubicek)]
 - Bob Cousins [[@bobc](https://github.com/bobc)]
 - Chris Palmer [[@nophead](https://github.com/nophead)]
 - David Braam [[@daid](https://github.com/daid)]
 - Edward Patel [[@epatel](https://github.com/epatel)]
 - Erik van der Zalm [[@ErikZalm](https://github.com/ErikZalm)]
 - Ernesto Martinez [[@emartinez167](https://github.com/emartinez167)]
 - F. Malpartida [[@fmalpartida](https://github.com/fmalpartida)]
 - Jochen Groppe [[@CONSULitAS](https://github.com/CONSULitAS)]
 - João Brazio [[@jbrazio](https://github.com/jbrazio)]
 - Kai [[@Kaibob2](https://github.com/Kaibob2)]
 - Luc Van Daele[[@LVD-AC](https://github.com/LVD-AC)]
 - Nico Tonnhofer [[@Wurstnase](https://github.com/Wurstnase)]
 - Petr Zahradnik [[@clexpert](https://github.com/clexpert)]
 - Thomas Moore [[@tcm0116](https://github.com/tcm0116)]
 - [[@alexxy](https://github.com/alexxy)]
 - [[@android444](https://github.com/android444)]
 - [[@benlye](https://github.com/benlye)]
 - [[@bgort](https://github.com/bgort)]
 - [[@ejtagle](https://github.com/ejtagle)]
 - [[@Grogyan](https://github.com/Grogyan)]
 - [[@marcio-ao](https://github.com/marcio-ao)]
 - [[@maverikou](https://github.com/maverikou)]
 - [[@oysteinkrog](https://github.com/oysteinkrog)]
 - [[@p3p](https://github.com/p3p)]
 - [[@paclema](https://github.com/paclema)]
 - [[@paulusjacobus](https://github.com/paulusjacobus)]
 - [[@psavva](https://github.com/psavva)]
 - [[@Tannoo](https://github.com/Tannoo)]
 - [[@teemuatlut](https://github.com/teemuatlut)]
 - ...and many others

## License

Marlin is published under the [GPL license](https://github.com/COPYING.md) because we believe in open development. The GPL comes with both rights and obligations. Whether you use Marlin firmware as the driver for your open or closed-source product, you must keep Marlin open, and you must provide your compatible Marlin source code to end users upon request. The most straightforward way to comply with the Marlin license is to make a fork of Marlin on Github, perform your modifications, and direct users to your modified fork.

While we can't prevent the use of this code in products (3D printers, CNC, etc.) that are closed source or crippled by a patent, we would prefer that you choose another firmware or, better yet, make your own.

[![Flattr this git repo](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=ErikZalm&url=https://github.com/MarlinFirmware/Marlin&title=Marlin&language=&tags=github&category=software)
