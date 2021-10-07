# PureData

A continuously evolving collection of tools, GUIs, FX and other stuff designed for PD Vanilla with no external library required.

## Prerequisites

* PureData Vanilla 0.46+ (no external libraries needed unless explicitly reported)

These patches/abstractions have been developed and tested on Windows 7/10 and Ubuntu Linux on Pd Vanilla 0.46 and up. I don't know if they work on previous versions or on other operating systems.

## Installing

Most of abstractions don't have dependancies, so you can use each of them by themselves except in few rare (where it is explicitly notified). Many patches depend on more than one abstraction and in that case it will be reported which one (most likely they are included in the same folder). Most of the abstractions come with an help patch.

To use them simply copy-paste the abstraction (and its dependancies) into you Pd working or search folder, then recall it with its name. You can eventually:
* Put the abstractions into the same folder as the patch that uses them.
* Put the abstractions into the extra folder of you Pd Vanilla installation.
* Create a new folder with the abstractions, then create a search path for that in Pd menu file->preferences->path...

## Content

`miniscope~`: mini oscilloscope to quickly probe a signal outlet.

`FunctionPlotter`: shows the plot of a function made of blocks or expr.

`FrequencyResponse~`: shows the amplitude frequency response plot of a filter.

`sliders`: array of 5, 10 and 20 vertical sliders, controllable with lists.

`makechord`: generate a series of midi notes given a chord shape and its root note.

`keyboard`: keyboards (88 or 128 keys) to show midi notes played by up to 4 different sources.

`Extras`: everything yet to be completed or that needs an help patch.