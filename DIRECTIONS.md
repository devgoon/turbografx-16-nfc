# TurboGrapx-16 Setup

## Prerequisites

1. Ensure Python 2.7 is working correctly and installed in `/usr/bin/python2.7`
2. `sudo apt-get install python-dev python-pip`

## Enable i2c device
1. `sudo mkdir /etc/nfc`
2. `sudo raspi-config`
3. Select "5 Interfacing"
4. Select "P5 I2C"
5. Select "\<Yes\>"
6. Exit `raspi-config` program
7. `sudo shutdown -r now` to reboot with i2c enabled.


## Install FEH
1. Ensure you are logged in as `pi` and in the `/home/pi` directory.
2. sudo apt-get install feh
3. cp -r turbograpx-16-nfc/art/cover ~/RetroPie/media
4. Run feh -Y -x -q -D 5 -B black -F -Z -z -r ~/RetroPie/media 

## Configure libnfc
1. `sudo nano /etc/nfc/libnfc.conf`
2. Cut and paste the following and save the file.
```
# Allow device auto-detection (default: true)
# Note: if this auto-detection is disabled, user has to manually set a device
# configuration using file or environment variable
allow_autoscan = true

# Allow intrusive auto-detection (default: false)
# Warning: intrusive auto-detection can seriously disturb other devices
# This option is not recommended, so user should prefer to add manually his/her device.
allow_intrusive_scan = false

# Set log level (default: error)
# Valid log levels are (in order of verbosity): 0 (none), 1 (error), 2 (info), 3 (debug)
# Note: if you compiled with --enable-debug option, the default log level is "debug"
log_level = 1

# Manually set default device (no default)
# To set a default device, users must set both name and connstring for their device
# Note: if autoscan is enabled, default device will be the first device available in device list.
device.name = "PN532"
device.connstring = "pn532_i2c:/dev/i2c-1"
```
3. Run `nfc-poll` and ensure you see `NFC reader: pn532_i2c:/dev/i2c-1 opened`
4. Try reading a tag, use Ctrl-C to stop or just wait 30 seconds

## Install nfc_poll
1. Ensure you are logged in as `pi` and in the `/home/pi` directory.
2. `export NFC_HOME=/home/pi/libnfc-1.7.1`
3. `git clone https://github.com/vminnocci/turbograpx-16-nfc.git`
4. `cd turbograpx-16-nfc/nfc`
5. `make`
6. `sudo make install`
7. Run `systemctl status nfc_poll` and ensure you see "Active: active (running)" in the output

## Configure your HuCards

In this system, the HuCards don't need to be written to, we configure a mapping to their UIDs, which should already be uniquely pre-programmed to each tag.

### Record your NFC tag UIDs
1. Run `tail -f /dev/shm/nfc_poll.log`
2. Place a HuCard (NFC tag) over the reader, the log should output "Reading NFC UID: 00000000000000" where the zeroes are the UID of the tag.
3. Copy/paste the UID into a text file.
4. Continue with all tags you wish to use.
5. To exit the log, hit \<Ctrl\>-C

### Record your desired games
1. `cd ~/RetroPie/roms`
2. Start typing `ls <system>/<name of game>` (e.g. `ls pcengine/Bonk`) to find the rom you want. Hit tab to complete the file, or hit tab twice to show possible matches. Don't forget to backslash things like spaces and parenthesis as you go.
3. After you finally tab through to the complete file, hit <enter>.
4. Copy the resulting line and put it and put it next to the UID you want to use in your text file. (`e.g. pcengine/Bonk's Adventure (USA).pce`) Make sure you don't have backslashes here.
5. Repeat this process

### Write your HuCards in the config
1. `sudo nano /etc/nfc_poll/nfc_poll.conf`
2. At the bottom of the file, there's a `[hucards]` section.
3. For each HuCard you want, add a line in this format: `<uid> = <game file>` (e.g. `00000000000000 = pcengine/Bonk's Adventure (USA).pce`)
4. `sudo systemctl restart nfc_poll`
5. Try it out! Place one of your HuCards on the reader and the screen should go black for a couple seconds, then bring up your game. Remove it and it should go back to the slideshow.

## Install screen_manager
1. Ensure you are logged in as `pi` and in the `/home/pi` directory.
2. (If you haven't already) `git clone https://github.com/vminnocci/turbograpx-16-nfc.git`
3. `cd turbograpx-16-nfc/screen`
4. `sudo make install`
5. Restart your Pi (try the reset button!) and if you've done all the steps above, everything should be working!

