# Booting G8OS on VirtualBox

The easiest and recommended approach is to boot from an ISO image you get from the [G8OS Bootstrap Service](https://bootstrap.gig.tech/). You get an ISO boot image using `https://bootstrap.gig.tech/iso/{BRANCH}/{ZEROTIER-NETWORK}` where:

- **{BRANCH}** is the branch of the CoreOS, e.g. `1.1.0-alpha`
- **{ZEROTIER-NETWORK}** is the ZeroTier network ID, create one on https://my.zerotier.com/network

See the [ISO section in the G8OS Bootstrap Service documentation](../bootstrap/bootstrap.md#iso) for more details on this.

Alternatively you can build your own boot image and create your own boot disk as documented in [Building your G8OS Boot Image](building/building.md).

Once you got your boot image, continue following the next steps:

- [Create a new virtual machine on VirtualBox](#create-vm)
- [Create a port forward from the VM to your host to expose the Redis of the core0](#create-portforward)
- [Start the virtual machine](#start-vm)
- [Ping the core0](#ping-core0)


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
