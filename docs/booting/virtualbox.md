# Booting G8OS on VirtualBox

Steps:

- [Build a G8OS boot image](#build-image)
- [Create a G8OS boot disk](#create-bootable)
- [Create a new virtual machine on VirtualBox](#create-vm)
- [Create a port forward from the VM to your host to expose the Redis of the core0](#create-portforward)
- [Start the virtual machine](#start-vm)
- [Ping the core0](#ping-core0)


<a id="build-image"></a>
## Build a G8OS boot image

See [Building your G8OS Boot Image](building/building.md).


<a id="create-bootable"></a>
## Create a G8OS boot disk

Using the G8OS boot image created in the previous step, you can easily create the G8OS boot disk as following:

```shell
dd if=/dev/zero of=g8os.img bs=1M count=90
mkfs.vfat g8os.iso
mount g8os.iso /mnt
mkdir -p /mnt/EFI/BOOT
cp staging/vmlinuz.efi /mnt/EFI/BOOT/BOOTX64.EFI
umount /mnt
```

<a id="create-vm"></a>
## Create a new virtual machine on VirtualBox  

Select a Linux 64bit:  

![create vm](images/create_vm.png)  

Before starting the virtual machine make sure you enabled the EFI support in the settings of the virtual machine:  

![create vm](images/enable_efi.png)  


<a id="create-portforward"></a>
## Create a port forward from the VM to your host to expose the Redis of the core0

![port forward](images/portforward.png)

<a id="start-vm"></a>
## Start the VM

Use the boot disk created in the second step as boot disk.

<a id="ping-core0"></a>
## Ping the core0

Using the Python client:

```python
import g8core
cl = g8core.Client('{host-ip-address}', port=6379, password='')
cl.ping()
```
