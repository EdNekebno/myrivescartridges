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

This should produce the default ZX Spectrum boot screen:

![Default Boot](https://github.com/EdNekebno/myrivescartridges/blob/main/images/default-boot.png)

### Games

To play a game, you need to have the .z80 or .tap file in the same folder. If you don't already have one these files, you can find them for your favorite games on sites like [World of Spectrum](https://worldofspectrum.org/) and [Spectrum Computing](https://spectrumcomputing.co.uk/). If the emulator finds just one game to play, then rather than the default boot it will start that game. This is so that when you make a rives cartridge it will auto start the game you want. When choosing games, you'll have the most success with 48k games in .z80 format. If you put one in the folder and run the command again it will start the game. For example, if I put dizzy.z80 in the same folder, I get the following when I run it.

![Dizzy](https://github.com/EdNekebno/myrivescartridges/blob/main/images/dizzy.png)

If you have more than one playable game in the folder, you will get the game selection menu

![Game Selection Menu](https://github.com/EdNekebno/myrivescartridges/blob/main/images/gameselectionmenu.png)

You can navigate this with the arrow keys and use ENTER to select your game. This is useful as you inevitably build up multiple games locally! The same is true if you put multiple games in a rives cartridge, but that's not advised as it negates some of the features of rives that we'll come to later in this guide.

##### Converting .tap files to z80 files

.z80 files are snapshots that start at whatever point they are taken. That's why it's preferable to use those as the player's game just starts. With .tap files you must load the tape. The emulator will boot to the standard +2 spectrum screen but with the file loaded as the tape. The best option is to use 48k mode (use SHIFT 6) to move down, hit ENTER, then at the prompt hit J, which will type LOAD for you, and ALT+P twice for the quotation marks.

![Loading a Tap File](https://github.com/EdNekebno/myrivescartridges/blob/main/images/loadquotequote.png)

Hit ENTER and if everything is good, the game should load.

It's so preferable to use .z80 snapshot files that the emulator has a little trick. Once your game is running, hit F3 and it will output a .z80 snapshot called dump-0.z80 (if that already exists then it chooses dump-1.z80, etc). You can check this file works, and delete the original .tap file, happy that you no longer need to type LOAD ""





THIS DOCUMENT IS A WORK IN PROGRESS. TO BE CONTINUED!
