# PXE

We assume you already have a working PXE Boot Environment (dhcp and tftp server).

In order to boot the G8OS kernel via PXE, you can use the popular `PXELINUX` tools.

# Configuration
- On your root tftp directory, create a new directory called `g8os` and put the `vmlinuz.efi` on it.
- Configure the bootfile as well:
```
DEFAULT 1
TIMEOUT 100
PROMPT  1

LABEL 1
    kernel g8os/vmlinuz.efi
```
- Save that config under `pxelinux.cfg/default` to run all your devices under G8OS.

# Per device PXE Boot
If you want to boot only some devices, you can symlink a special config for that MAC Address. Let assume you've put the config above on a `pxelinux.cfg/g8os`, on the `pxelinux.cfg` directory, run:
```
ln -s g8os 01-2c-88-88-cd-2a-01
```