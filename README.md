# IC705MultiMeter
![basic](https://img.shields.io/badge/M5Stack-BASIC-blue)
![grey](https://img.shields.io/badge/M5Stack-GREY-blue)
![fire](https://img.shields.io/badge/M5Stack-FIRE-orange)
![core2](https://img.shields.io/badge/M5Stack-CORE2-green)
![aws](https://img.shields.io/badge/M5Stack-AWS-orange)

![licence](https://img.shields.io/github/license/armel/IC705MultiMeter)
![language](https://img.shields.io/github/languages/top/armel/IC705MultiMeter)
![size](https://img.shields.io/github/repo-size/armel/IC705MultiMeter)
![version](https://img.shields.io/github/v/release/armel/IC705MultiMeter)
![activity](https://img.shields.io/github/commit-activity/y/armel/IC705MultiMeter)

**An excellent [video](https://www.youtube.com/watch?v=SCPEO7Eiy1E&ab_channel=HAMRADIODUDE) was released by @HamRadioDude about the installation of the IC705SMeter project. It can help you ! This is the same approach here.** 

The IC7505MultiMeter project allows you to display the equivalent of the Meter screen of the IC705, directly on the M5Stack screen. This allows you to dedicate the IC705 screen to the Waterfall while having all the measurements on the M5Stack screen.

![IC705MultiMeter FM](https://github.com/armel/IC705MultiMeter/blob/main/img/FM.png)
![IC705MultiMeter SSB](https://github.com/armel/IC705MultiMeter/blob/main/img/SSB.png)

# Technical architecture

## Quick overview

[M5Stack](https://m5stack.com/) is based on an ESP-32, dual core, which can be clocked up to 240 MHz. M5Stack has 16 MB of flash memory. Like all ESPs, Wi-Fi is of course integrated. The 2 inch IPS color display, based on the ILI9342C chipset, has a comfortable resolution of 320 x 240 pixels. It is very bright. The integrated battery is 110 mAh. It is possible to add an additional battery (700 or 800mAh) if needed.

In terms of size and weight, it is very compact: 54 x 54 x 18mm for 47.2g. Can be carried in the pocket without any problem ;)

## Detailed technical specs

Here are the detailed technical specs, for the curious:

| Resources |	Description |
| --------- | ------------ |
|ESP32| 240MHz dual core, 600 DMIPS, 520KB SRAM, Wi-Fi, dual mode Bluetooth
Flash| Memory	16MB|
|Power| Input	5V @ 500mA|
|Port|	TypeC x 1, GROVE(I2C+I/0+UART) x 1|
|Core|Bottom Port	PIN (G1，G2，G3，G16, G17, G18, G19, G21, G22, G23, G25, G26, G35, G36)|
|IPS Screen|	2 inch, 320x240 Colorful TFT LCD, ILI9342C, max brightness 853nit|
|Button|	Custom button x 3|
|Speaker|	1W-0928|
|Battery|	110mAh @ 3.7V|
|Antenna|	2.4G 3D Antenna|
|Operating Temperature|	32°F to 104°F ( 0°C to 40°C )|
|Net weight|	47.2g|
|Gross weight|	93g|
|Product Size|	54 x 54 x 18mm|
|Package Size	|95 x 65 x 25mm|
|Case Material|	Plastic ( PC )|

## In addition

About the QSJ, count around 45€. You then have a complete development platform, totally autonomous, programmable in C and C++, MicroPython and UIFlow, from Linux, Windows or MacOS, all in a compact and ultra ergonomic box.


# Installation

## Prepare the stack

The easiest way is to install [PlateformIO for VSCode](https://platformio.org/install/ide?install=vscode) on your PC (Linux or Windows) or on your Mac (Intel or M1). It is a cross-platform and multilanguage development environment that is powerful and pleasant to use.

Then, still on your PC or Mac, clone the IC705MultiMeter project via the command :

`git clone https://github.com/armel/IC705MultiMeter.git`

You can also download a [zip archive](https://github.com/armel/IC705MultiMeter/releases) of the project, if you prefer, and unzip it.

As I said, an excellent [video](https://www.youtube.com/watch?v=SCPEO7Eiy1E&ab_channel=HAMRADIODUDE) was released by @HamRadioDude about the installation of the IC705SMeter project. It can help you ! This is the same approach here.

## Configuration

Open the IC705MultiMeter project with PlateformIO for VSCode.

### File `src/settings.h`

#### Model of M5Stack

Line 5, check that the constant `BOARD` corresponds to your M5Stack model (by default, the constant is initialized to `BASIC`). So, indicate : 

- `BASIC` if you have an M5Stack BASIC

```
#define BOARD BASIC
```

- `GREY` if you have an M5Stack GREY

```
#define BOARD GREY
```

- `CORE2` if you have an M5Stack CORE2

```
#define BOARD CORE2
```

#### Bluetooth Address of your IC705

Line 8, change the address of your IC705 if necessary. I have indicated the default value. Refer to the documentation, if needed.

#### Wifi Configuration 

Line 11 and 12, indicate your SSID and your Wifi password. You can view your IC705MultiMeter from a simple browser. It is even possible to control it by this way, as the buttons are clickable. In order to display your IC705MultiMeter in your browser, just go to `http://ip_address_of_your_ic705multimeter/`. As a reminder, the IP address that your IC705MultiMeter retrieves is displayed on the screen.

> Beware: it's slow! And there is no automatic refresh. You have to click on the background of the screen image to make a new capture. And otherwise, as said, the buttons are functional.

### File `platformio.ini`

If and only if __you are using the M5Stack Core2__, edit the `platformio.ini` file and modify the lines,

```
default_envs = m5stack-basic-grey
;default_envs = m5stack-core2
```

By,

```
;default_envs = m5stack-basic-grey
default_envs = m5stack-core2
```

This is the same as changing the target platform, the semicolon being a comment.

## Compiling and flashing the M5Stack

Compile and upload the project to your M5Stack. You are done !

# Usage

Once launched, you must connect your IC705 to your M5Stack via the menu (Set / Bluetooth Set) of your transceiver. Refer to the documentation, if needed.

In addition :

- a long press on the left button allows to decrease the brightness, 
- a long press on the central button allows to switch off the M5Stack,
- a long press on the right button allows to increase the brightness.

> The value of the brightness is preserved at the next restart.

# Using the Bin Loader (power user only...)

It's possible to store several applications on the SPI Flash File Storage of your M5Stack or on SD Card Storage. At startup, a procedure is provided to load a particular application.

## Preparation

I will detail here the procedure to deploy IC705SMeter and IC705MultiMeter applications on the same M5Stack.

### Step 1 - Compile

Start by compiling your applications, as you used to do. Nothing changes here. For example, start by compiling the IC705SMeter application. Then do the same with the IC705MultiMeter application. 

### Step 2 - Collecting the binary files

That's it, you have compiled the IC705SMeter and IC705MultiMeter application? It's perfect.

Each compilation has produced a binary. It is this binary that is sent / flashed to your M5Stack, via the USB connection.

Go to the root of the IC705SMeter folder, which contains the whole project. And go to the :

- `.pio/build/m5stack-basic-grey`, if you compiled for a GREY or BASIC M5Stack
- `.pio/build/m5stack-core2`, if you compiled for M5Stack CORE2 or AWS

You will find a `firmware.bin` file there. Now, there are 2 solutions...

### Step 2.1 - SD Card Storage (simple)

Format an SD Card as FAT32.

Copy the `firmware.bin` at the root of the SD Card. And take the opportunity to rename it, for example, `IC705SMeter.bin`.

Do the same with the IC705MultiMeter application. Of course rename it with a different name, for example, `IC705MultiMeter.bin`.

At this point, you should have 2 clearly identified binaries in the root of your SD Card : `IC705SMeter.bin` and `IC705MultiMeter.bin`.

### Step 2.2 - SPI Flash File Storage (more difficult)

Copy `firmware.bin` in the `data` directory at the root of the IC705SMeter folder. And take the opportunity to rename it, for example, `IC705SMeter.bin`.

> If the `data` folder does not exist, create it.

Do the same with the IC705MultiMeter application. Go to the root of the IC705MultiMeter folder, which contains the whole project. And go to the directory :

- `.pio/build/m5stack-basic-grey`, if you have compiled for a M5Stack GREY or BASIC
- `.pio/build/m5stack-core2`, if you compiled for M5Stack CORE2 or AWS

You will also find a `firmware.bin` file. Copy it, too, in the `data` directory at the __root of the IC705SMeter folder__. And take the opportunity to rename it to, for example, `IC705MultiMeter.bin`.

> Important, the idea is to copy these 2 binaries in the same directory `data`** (located at the root of the IC705SMeter folder).

At this point, you should have 2 clearly identified binaries: `IC705SMeter.bin` and `IC705MultiMeter.bin` in the `data` directory at the root of the IC705SMeter folder.

So let's move on to what is probably the most complicated step. Open the IC705SMeter project from Visual Studio Code, as you would compile it. 

![Capture](https://github.com/armel/RRFRemote/blob/main/img/flash_1.png)

Step 1, click on the Platformio icon (the icon with an ant's head...). Step 2, unroll the section :

- `m5stack-basic-grey`, if you have compiled for an M5Stack GREY or BASIC
- `m5stack-core2`, if you compiled for M5Stack CORE2 or AWS

![Capture](https://github.com/armel/RRFRemote/blob/main/img/flash_2.png)

Finally, step 3, go to the `Platform` sub-section. And click on `Upload Filesystem Image`.

Wait ! It's coffee time (or beer) :) The contents of the `data` directory will be written to the SPI Flash File Storage of your M5Stack. Are you done? You're there !!!!

## Usage

Start your M5Stack. You should see a black screen, followed by 1, 2 and 3 small dots at the top of the screen. This is the famous Bin Loader ;)

As soon as the first little dot appears, you can :

- either press the left or right button, to launch the default application.
- or press the central button. In this case, the Bin Loader menu appears and offers you the list of available binaries in SPI Flash File Storage or SD Card. 

If you have followed the procedure perfectly, you should have a choice between `IC705SMeter.bin` and `IC705MultiMeter.bin`.

The left and right buttons allow you to switch from one binary to another. And the middle button validates the selected binary. In this case, the selected application will be loaded ;)

> The loading takes about 20 seconds...

## Limitation

I think it is possible to have 3 or 4 applications cohabit in SPI Flash File Storage. If need more, use SD Card Storage.

# Donations

If you find this project fun and useful then [offer me a beer](https://www.paypal.me/F4HWN) :) 

By the way, you can follow me on [Twitter](https://twitter.com/F4HWN) and post pictures of your installation with your M5Stack. It always makes me happy ;) 