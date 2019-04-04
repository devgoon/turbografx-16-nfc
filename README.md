# TurboGrapx 16 w/ NFC
Support code for my version of a RPi-based Turbograpx 16

This is based on/inspired by [Coderkevin](https://github.com/coderkevin/mini-nes). Thank you Kevin!
- Even simpler version of Coderkevin's work with a focus on a TG-16
- "HuCard" art sized for NFC Cards NTAG216 
- Support for toggle switch power up/down using [Mausberry Switch](https://mausberry-circuits.myshopify.com/pages/soldering-your-own-switch)


Here's a more detailed list of the features:

## NFC Hucard support

The NFC Reader is a PN532 running on the RPi's i2c interface. I've made a simple c interface to Python to utilize it. No Arduino or microcontroller needed to use it.

## No NFC tag writing needed

This system is designed to simply rely on the unique IDs already imprinted on your NFC tags. It uses a configuration file to map those UIDs to the correct game files to be run.

## Immediate loading of games

The system does not have to be powered off to start a game. It continually scans for hucards and will restart Emulation Station as soon as a cart is installed. Don't worry if you like the feel of the old process though. You can still power off the system and install your cart and power it back on if you like.

## Using factory on/off switch
In an attempt to keep the original console looking stock we will using a [Mausberry switch]([Mausberry Switch]https://mausberry-circuits.myshopify.com/pages/soldering-your-own-switch)

## Using original controller
Using [Bliss-Box Pro](https://bliss-box.net/store/Gamer-Pro-Kit-p129163061) with TG16 large dongle and [Old Skool](https://www.oldskoolgames.com/product-page/turbografx-16-pc-engine-controller) aftermarket controller