
# System76 PopOS on Dell XPS 15 7590 OLED 2019

This page will explain how to fix a number of issues with **System76 PopOS 20.04**. but overall I recommend using **PopOS** rather than **Ubuntu** because it comes with below support: 
**Note:** PopOS is based on Ubuntu, so no worries no new learning curve :)
- Nvidia cards support out of the box, actually when you do to the download page you can choice an image for Nvidia or AMD/Intel
- It have Power profiles out of the box(Battery life/balance/high performance)
- the most important one is OLED support. you don't have to wright a script or do anything to make it work

Now let's talk about the small issues we are going to fix 
 
Problems addressed are:

- Suspend Draining battery fast

Problems not addressed yet:
- ability to hibernate

## 1- Installing System76 PopOS (assuming only System76 PopOS, not dual boot)

1. Download [System76 PopOS 20.04](https://pop.system76.com/)
2. Create Bootable usb stick using `Rufus` on Windows or `Disks` on Ubuntu 
3. Change `SATA Mode` inside `BIOS(UEFI)` from `RAID on` to `AHCI`, this is done though: 
	- `Power up` your machine
	- click `f12` 
	- choice `BOIS Configurations`.  
4. Restart your machine then click `f12` again, then choice to boot from the usb stick.
5. Follow System76 PopOS installation window, or play with it first.
6. After the installation is complete, run
	```
	sudo apt update
	sudo apt dist-upgrade -y
	```
	to update the system to the latest versions.

## 2- Suspend Draining battery fast
By default, the very inefficient `s2idle` suspend variant is incorrectly selected. This is probably due to the BIOS. The much more efficient `deep` variant should be selected instead.

#### One time fix
It is possible to change the suspend mode from the command line via.
```
echo deep| tee /sys/power/mem_sleep
```

#### Permanent fix:
`System76 PopOS` uses `kernelstub` to manage the boot parameters and kernel images, instead of `GRUB`.

1. open terminal window
2. run `sudo kernelstub --add-options "mem_sleep_default=deep"`
3. enter your password
4. reboot


## 3- Useful Packages:
1. [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/) (gnome extension)

