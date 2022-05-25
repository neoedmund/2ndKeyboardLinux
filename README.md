# 2ndKeyboardLinux
Use 2nd keyboard as function keypad in Linux

A multi-keyboards aware X hotkey daemon 

![img](https://github.com/neoedmund/2ndKeyboardLinux/blob/main/kb3.jpg?raw=true)

This tool is used to customize an 2nd keyboard as function keypad in Linux xorg desktop. 
But you still can make it used on a single keyboard.

First things first , you can download and try, to see if it works on your system. 
Also try to edit the config file to fit your needs.

Currently the source is not released yet, if you feel like it, make a star★. 
if the project gathered a lot of starts, I will release the source .

## Steps:
1. plug 2 keyboards of course 

1.1 clone this repo by `git clone "https://github.com/neoedmund/2ndKeyboardLinux"`

2. `xinput` to find out the device name of the keyboard 
```
  xinput

⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ ELECOM BlueLED Mouse                    	id=8	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Power Button                            	id=7	[slave  keyboard (3)]
    ↳ SINO WEALTH USB KEYBOARD                	id=9	[slave  keyboard (3)]
    ↳ SINO WEALTH USB KEYBOARD System Control 	id=10	[slave  keyboard (3)]
    ↳ SINO WEALTH USB KEYBOARD Consumer Control	id=11	[slave  keyboard (3)]
    ↳ USB KEYBOARD USB KEYBOARD System Control	id=13	[slave  keyboard (3)]
    ↳ USB KEYBOARD USB KEYBOARD Consumer Control	id=14	[slave  keyboard (3)]
    ↳ Eee PC WMI hotkeys                      	id=15	[slave  keyboard (3)]
    ↳ USB KEYBOARD USB KEYBOARD               	id=12	[slave  keyboard (3)]
```

2.1  use `xinput --disable 12` (for instance "USB KEYBOARD USB KEYBOARD") to disable the 2nd keyboard, so keystrokes on it will not received by X


3. edit the config file `evtest3.conf` and copy to your home directory by `cp evtest3.conf ~/`

4. it runs need JDK, so install JDK into /opt or using package manager of your disto like `apt install default-jdk`

5. run the program `./evtest3.exe`  don't confused by its file extension , it's for Linux.

## the config file
```
{
	mapping : {
		"AT Translated Set 2 keyboard" : [
			[ [ 56 115 125 ] [ keys ctrl-c ] reversedReleaseOrder ] /*elitebook phone up*/
			[ [ 29 56 114 ] [ keys ctrl-v ] reversedReleaseOrder ] /*elitebook phone down*/
		]
		"USB KEYBOARD USB KEYBOARD" : [
			[ [ 94 ] [ keys ctrl-c ] ] /*MUHEN*/
			[ [ 92 ] [ keys ctrl-v ] ] /*HENKAN*/
			[ [ 57 ] [ keys F9 ] ] /*space*/

			[ [ 59 ] [ exec [ neoeedit ] ] ] /*F1*/
			[ [ 60 ] [ exec [ jfe ] ] ] /*F2*/
			[ [ 61 ] [ exec [ firefox ] ] ] /*F3*/
			[ [ 99 ] [ exec [ nb -run jscreenshot -main neoe.tools.Screenshot ] ] ] /*Print Screen*/
		]
	}
}
```

it is quite self explanatory .
for the key codes, you can run `evtest3.exe` first and press the keystroke and see the code printed out on the console .

it support 2 commands: 

`keys` for simulate keystroke and

`exec` to execute command line with args.

## troubleshooting 
if `evtest3.exe` not reading the `/dev/input/event*` it maybe because of permissions . you can try run with `sudo ./evtest3.exe`

Last, feel free to ask question or bug reports in the issue section!


