# PureData Tools

A continuously evolving collection of tools, GUIs, FX and other stuff designed for Pd Vanilla with no external library required.

_Note: Some stuff in `vst` and `modular` folder has been created with Pd-Extended and is not quite vanilla yet so it may require `[mknob]` from moonlib to work. The GUI will be updated in the future to avoid that dependency._

## Prerequisites

* PureData Vanilla 0.46+

These patches/abstractions have been developed and tested on Windows 7/10 starting from Pd Vanilla 0.46 and should be working fine on Unix and MacOS and in other/newer versions and flavors of Pd.

## Installing

Most of the abstractions don't have dependencies, except for some of the GUI ones that still require `[mknob]` and are anyway going to drop that dependency in the near future as well. At most some object will require some other ones from this repository so feel free to download and drop them all in the same folder if you prefer. Or best, add each folder to the search path of your Pd installation to keep things tidy.

## Content

`biquad_filters`: Filters automating the creation of coefficients for the biquad filter.

`color_tools`: simple utilities to calculate or show Pd color value from standard RGB values.

`frequency_response`: shows the amplitude frequency response plot of a filter.

`function_plotter`: shows the plot of a function made of blocks or expr.

`fx`: simple audio effects, made for guitar but suitable for any kind of audio signal

`gui`: many objects with a GUI to make stuff in Pd a little more visual.

`keyboard`: keyboards (88 or 128 keys) to show midi notes played by up to 4 different sources.

`keykey`: an object that intecepts keyboard events and generates MIDI notes making the keyboard act as a piano MIDI keyboard.

`makechord`: generate a series of midi notes given a chord shape and its root note.

`miniscope`: mini oscilloscope to quickly probe a signal outlet.

`modular`: a collection of modular eurorack style GUI objects.

`sliders`: array of 5, 10 and 20 vertical sliders, controllable with lists.

`osc_examples`: example to use the OSC protocol to communicate with the outer world.

`preset`: objects used to save and load presets using Pd messages.

`utils`: many objects to do lots of different stuff.

`vst`: self-contained objects with a GUI acting like classic VSTs in DAW applications.