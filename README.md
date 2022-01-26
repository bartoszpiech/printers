# Installing CUPS, Canon iR2520, HP Officejet Pro 8100 on Artix Linux

In this gist I'll try to explain how to install printing software and drivers
needed for Canon iR2520 and HP Officejet Pro 8100 printers that I use at home /
in work. This tutorial is written for people using Artix Linux or other Arch
forks. I am using **runit** init and service daemon, so if You use
openrc/s6/systemd or other init system, you'll have to tweak some things,
especially when starting/enabling CUPS service. All printers are configured to
work through the network. Additionally in the future I'm planning to write some
shell script to do this automatically.

## CUPS

To download and install CUPS and enable it's services, you'll need root
privileges and some internet connection.

First, update your packages.
```bash
$ sudo pacman -Syu
```
Then get cups packages from official Arch/Artix repositories.
```bash
$ sudo pacman -S cups cups-runit
```
Finally, after all packages have been installed, add the CUPS service.
```bash
$ sudo ln -s /etc/runit/sv/cupsd/ /run/runit/service/
```
And start the CUPS service.
```bash
$ sudo sv start cupsd
```

Now, after starting the CUPS service you can access it via the web browser
through port 631 using [localhost].

## HP Officejet Pro 8100

Most modern HP drivers are in the **hplip** package. You can check if your
printer model is supported via [this HP site]. To install HP drivers on your
machine you have to get this package from the official Arch repository.
```bash
$ sudo pacman -S hplip
```
After installing you can easily add your printer via CUPS web user interface.


## Canon imageRunner 2520

This printer uses UFRII drivers, so you'll have to install **cnrdrvcups-lb**
package via [Arch User Repository]. I'm using yay AUR helper, so if you use it
you can follow along. To install those drivers you don't need root privileges.
```bash
$ yay -S cnrdrvcups-lb
```

Now you can add the printer and set it's settings accordingly


## TODO
- [x] Write the tutorial/README,
- [ ] add the shell script,
- [ ] test script using VM/Docker,
- [ ] extend the tutorial for Windows/OSX.


[localhost]: http://localhost:631
[this HP site]: https://developers.hp.com/hp-linux-imaging-and-printing/supported_devices/index
[Arch User Repository]: https://aur.archlinux.org/
