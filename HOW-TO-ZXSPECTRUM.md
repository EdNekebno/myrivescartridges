# ZX Spectrum Emulator for RIVES.io

The file zxspectrum.sqfs contains a ZX Spectrum emulator in the sqfs cartridge format for rives. You can try it out by download zxspectrum.sqfs and going to [emulator.rives.io](https://emulator.rives.io) and dragging it to where it says "Drop Cartridge .sqfs file".

Naturally if you do that you'll just get a ZX Spectrum emulator, and what we all want to do is play games. But first a quick description of the emulator capabilities.

## Emulator Spec

* Emulators a Sinclair ZX Spectrum 48k and 128k (+2)
* Should run in realtime, 50fps, on most systems
* Emulates a 48k spectrum with sampled virtual speaker
* Emulates a 128k spectrum (but struggles with AY chip emulation)
* Game Controller acts as Kempson Joystick
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

##### Making a RIVES cartridge

Okay, so you can now play spectrum games. That's pretty cool. But we want to take advantage of rives features. In particular the ability to record the score. It would also be cool if we could use a game controller with the games. Got you covered!

###### Scores and Game Over Screens

Load up a game and hit F1. You'll see a menu pop up. There's quite a few options, so as you'll guess these instructions are going to be quite long :) 

![Game Config for RIVES](https://github.com/EdNekebno/myrivescartridges/blob/main/images/gameconfigforrives.png)

With the exception of turning sound on and off (useful for 128k mode), these relate to the score and the end game. For this example, I'll use the game 3D Death Chase. The first thing I'll do is set the score location. These are represented by zeros and then an X in the position we're looking for. So if I select 00000X then I'm looking for the last digit. Use the arrows keys to select that and hit enter and you get:

![Location Selector](https://github.com/EdNekebno/myrivescartridges/blob/main/images/locationselector.png)

This looks like just a 3D Death Chase screen, but if you look carefully at the top left there's a box outlined in magenta. We can use the arrow keys and enter to select the square on the screen where this number is. Most of the time the whole number fits in this square, but if it doesn't then select the square with the most of the number.

![Select last digit in score](https://github.com/EdNekebno/myrivescartridges/blob/main/images/selectlastscore.png)

Here we go, I've put the box over the last digit in the score and if I hit enter, it will go back to the main menu. This magenta box comes up a lot for items in this menu. Also for 0000x0 for the second to last digit, and so on.

Once the score locations are saved, it's probably a good idea to use the arrow keys to select "Save Config File" and hit enter. It'll beep when it's saved it.

Next notice that there are several menu items like "SET SC NUM x HASH". Now we've set where the score locations are, we need to tell the emulator how to recognise a each possible digit of the score. Basically, we're teaching it what a zero looks like, what a 1 looks like, and so on. Normally this involves going to the "back to the emulator" menu item and playing the game a bit until you have scores containing 0, 1, etc. So you go backwards and forwards a bit but it's not too tough. With 3D Death Chase the score is shown as zeros before you even start. So I can choose "SET SC NUM 0 HASH: 0" and hit enter, position the magenta square over any number 0 in the score and hit enter. 

You'll see the number next to the menu item change.

![SC 0 Hash](https://github.com/EdNekebno/myrivescartridges/blob/main/images/sc0hash.png)

This is a hash, it's a kind of magic number that allows the emulator to recognise the zero in the scores. When you've done all digits (0 to 9), the menu will look something like this (but probably with different hash numbers)

![SC Hashes](https://github.com/EdNekebno/myrivescartridges/blob/main/images/schashes.png)

A handy hit is all the numbers should be different. Now's probably a good time to save the config file again.

Next it's time to do something I excel in in games - lose! Let the game play and deliberately die and hit F1 when the game shows a game over screen. There are four options at the top. SET ENDGAME MIN X, SET ENDGAME MIN Y, SET ENDGAME MAX X, SET ENDGAME MAX Y. We actually only need to use two of these as the min and max options set both the X and Y regardless of which you pick. For my example, I'm going to hit SET ENDGAME MIN X.

![Game Over Min](https://github.com/EdNekebno/myrivescartridges/blob/main/images/gameovermin.png)

We need to find something unique about this game over screen that will be the same every time. The min options let us set the top left of the bounding box. Here it's just the text "GAME OVER", that's all on the same line. So I put the box at the beginning and hit enter.

Back in the main menu you'll see it's filled in the MIN X and the MIN Y values for you. Do the same with the SET ENGAME MAX X option. In my case I'd position the box over the "R" in over, but it may be that you should select a bigger area with different games.

Time to save the config file one more time. The emulator now knows how to tell rives when the game is over and what the score was.

###### Game Controller

We've come along way since the decades old speccy key. We probably want to use a game controller (or at least map the keys RIVES uses for one to whatever weird speccy keys the game author choose). The Game Controller will also emulate a Kempston joystick, but we should do this anyway. Hit F2 and you get a different menu.

![Key Config](https://github.com/EdNekebno/myrivescartridges/blob/main/images/keyconfig.png)

This is super easy. Find out what keys the game uses. I have two favourite methods I use for this. The first is just randomly pressing keys on the keyboard and seeing if they do anything, the second I call Google :) Select the game controller item on the menu with the up down arrows, hit enter, wait for the confirmation sound and then hit whatever key you want to map to the item on the controller.

![Death Chase Keys](https://github.com/EdNekebno/myrivescartridges/blob/main/images/deathchasekeys.png)

Here I have mapped the, I imagine logical to somebody, keys for 3D death chase to the appropriate controller buttons. Note: you can have multiple game controller buttons send the same key - hence I set a lot of them to be space for fire!

Time to hit "SAVE CONTROLLER CONFIG" and we're all done with configuration. The emulator can now tell rives the game is over, what the score was, and you can use the game controller.





THIS DOCUMENT IS A WORK IN PROGRESS. TO BE CONTINUED!
