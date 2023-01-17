# Waydroid Magisk
Install and manage Magisk Delta in waydroid. 

- [Waydroid Magisk](#waydroid-magisk)
- [Installing Magisk on Waydroid](#installing-magisk-on-waydroid)
  - [Requirements](#requirements)
  - [Installation](#installation)
    - [From PPA](#from-ppa)
    - [From GitHub](#from-github)
- [Usage](#usage)
- [FAQ](#faq)
  - [What does work?](#what-does-work)
  - [Waydroid won't start](#waydroid-wont-start)
  - [No internet connection](#no-internet-connection)
  - [Magisk modules not working or not showing as installed](#magisk-modules-not-working-or-not-showing-as-installed)
  - [Updating](#updating)
  - [Does this survive Waydroid updates?](#does-this-survive-waydroid-updates)
  - [Does Zygisk work?](#does-zygisk-work)
  - [I've enabled Zygisk in Magisk Delta Stable, updated waydroid images!!](#ive-enabled-zygisk-in-magisk-delta-stable-updated-waydroid-images)
  - [How is this different from other scripts?](#how-is-this-different-from-other-scripts)
  - [What is Magisk Delta?](#what-is-magisk-delta)
  - [Arch Linux](#arch-linux)

# Installing Magisk on Waydroid

## Requirements
* waydroid
* make
* git

## Installation
### From PPA
1. `curl -s --compressed "https://nitanmarcel.github.io/waydroid-magisk/waydroid_magisk.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/waydroid_magisk.gpg > /dev/null`
2. `sudo curl -s --compressed -o /etc/apt/sources.list.d/waydroid_magisk.list https://nitanmarcel.github.io/waydroid-magisk/waydroid_magisk.list`
3. `sudo apt update`
4. `sudo apt install waydroid-magisk` 
5. run `sudo waydroid_magisk --install` to install Magisk
6. **To avoid any issues it's important to read [FAQ](#faq) before using Magisk Delta on waydroid.**

### From GitHub
1. git clone `https://github.com/nitanmarcel/waydroid-magisk-installer/`
2. run `sudo make install USE_SYSTEMD=1`
  * If using upstart (e.g Ubuntu Touch 16.04)
  * run `sudo make install USE_UPSTART=1`
3. run `sudo waydroid_magisk --install` to install Magisk
  * Ubuntu Touch requires setting an working directory in `/home/phablet`
    * `sudo waydroid_magisk --install /home/phablet/magisk_waydroid`
4. enable ota survival service
  * For systemd `sudo systemctl enable waydroid_magisk_ota.service && sudo systemctl start waydroid_magisk_ota.service`
  * For upstart `sudo start waydroid_magisk_ota.service`
5. **To avoid any issues it's important to read [FAQ](#faq) before using Magisk Delta on waydroid.**

# Usage

```
options:
  -h, --help            show this help message and exit
  -i [INSTALL], --install [INSTALL]
                        Install Magisk Delta in Waydroid
  -r, --remove          Remove Magisk Delta from Waydroid
  -o, --ota             Handles OTA updates in Waydroid with Magisk Delta
  --install-module INSTALL_MODULE
                        Installs a Magisk module
  --remove-module REMOVE_MODULE
                        Removes a Magisk module
  --list-modules        Lists all installed Magisk modules
  --su                  Starts Magisk SU inside waydroid.
```

# FAQ

## What does work?
* root
* zygisk
* modules
* updates
* ~~ota updates survival~~ (Starting with waydroid 1.4.0)

## Waydroid won't start
Note that Waydroid may take longer to boot due to Magisk being set up.

## No internet connection
Try restarting Waydroid using either systemd or init (depending on your system).

## Magisk modules not working or not showing as installed
Currently, modules only work with Magisk Delta Canary. Download and install the apk in Waydroid, and update by following the instructions in the "Updating" section below.

## Updating
Use Magisk Delta to install Magisk directly into the system partition. Always update through the Magisk app, not the `install.sh` script.

## Does this survive Waydroid updates?
If the Android system is updated, Magisk will be removed and you'll need to run `install.sh` again to reinstall it.

## Does Zygisk work?
Zygisk only works with Magisk Delta Canary which gets installed by default with `install.sh`. Enabling it with Magisk Delta Stable will result in waydroid not booting.Debug and updating waydroid as it will require running `install.sh` which reverts to stable magisk and will stop waydroid from booting. -->

## I've enabled Zygisk in Magisk Delta Stable, updated waydroid images!!
Delete `/data/adb/magisk.db` inside `waydroid shell`. Will clear Magisk's database and disable zygdisk.

## How is this different from other scripts?
* This script installs Magisk Delta, a fork of Magisk with some reimplemented features such as Magisk Hide and better support for Android emulators.
* It follows the same installation workflow as Magisk, allowing users to update through the Magisk Delta Manager instead of relying on the `install.sh` script from this repository.

## What is Magisk Delta?
Magisk Delta is a fork of the official Magisk Manager with the old Magisk Hide feature re-added and other new features. You can find a list of differences between Magisk Delta and official Magisk [here](https://github.com/HuskyDG/magisk-files/blob/main/note_stable.md#diffs-to-official-magisk).

## Arch Linux
linux-zen does not support Magisk Delta. Whatever, people reported that `linux-xanmod-anbox` with `linux-xanmod-anbox-headers` from chaotic AUR works without any issues. 
