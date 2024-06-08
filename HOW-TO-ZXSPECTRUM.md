#ZX Spectrum Emulator for RIVES.io

The file zxspectrum.sqfs contains a ZX Spectrum emulator in the sqfs cartridge format for rives. You can try it out by download zxspectrum.sqfs and going to [emulator.rives.io](https://emulator.rives.io) and dragging it to where it says "Drop Cartridge .sqfs file".

Naturally if you do that you'll just get a ZX Spectrum emulator, and what we all want to do is play games. But first a quick description of the emulator capabilities.

## Emulator Spec

* Emulators a Sinclair ZX Spectrum 48k and 128k (+2)
* Should run in realtime, 50fps, on most systems
* Emulates a 48k spectrum with sampled virtual speaker
* Emulates a 128k spectrum (but struggles with AY chip emulation)
* Can load .z80 snapshot files
* Basic .tap file support
* Can read the score of the screen and detect end of game for rives.io functionality

Most .z80 files should work. You can find lots on sites like [World of Spectrum](https://worldofspectrum.org/) and [Spectrum Computing](https://spectrumcomputing.co.uk/). When you have a choice it is preferable to download .z80 files. The emulator also has .tap file support. This hooks the spectrum load routines to load the data, so will work if the game uses the ROM routines.

## Playing locally or Preparing to make a cartridge file from a game

* Download the file zxspectrum.zip and uncompress it to a new folder
* [Use these instructions to Download and install rivemu into that folder](https://docs.rives.io/docs/riv/getting-started#installing)

You can test the spectrum works with

`./rivemu -workspace -exec ./zxspectrum`

This should produce the default ZX Spectrum boot:

![Default Boot](https://github.com/EdNekebno/myrivescartridges/blob/main/images/default-boot.png)
