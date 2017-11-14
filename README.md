# PureData

_WORK IN PROGRESS_ A collection of tools, GUIs, FX and other stuff designed for PD Vanilla without external libraries.

## Prerequisites

* PureData Vanilla 0.47 (no external libraries needed unless explicitly reported)

These patches/abstractions have been developed and tested on Windows 7/10 and Ubuntu Linux on Pd Vanilla 0.46 and up. I don't know if they work on previous versions or on other operating systems.

## Installing

Most of abstractions have no dependancy, so you can use each of them alone except in few rare cases and it will be notified. Many patches depends on more than one abstraction and in that case it will be reported which ones. Most of the abstraction come with a help patch but not all of them.

To use them simply copy-paste the abstraction (and its dependancies) into you Pd working or search folder, then recall it with its name. You can eventually:
* Put the abstractions into the same folder as the patch that uses them.
* Put the abstractions into the extra folder of you Pd Vanilla installation.
* Create a new folder with the abstractions, then create a search path for that in Pd file/preferences/path...

## Content

* GUI - a collection of graphic elements for a bit of eye-candy.
* FX - audio effects (tremolo, reverb, delay, pitch-shift, distortion...)
* TOOLS - conversion tools, math blocks, audio math stuff and other things.
* CONTROLS - midi and osc control blocks, triggers, sequencers and others.
* VST - a series of GUI based elements that work just like VSTs.
* PATCH - collection of patches that use many different abstractions.

### License
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
