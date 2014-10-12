## Realtek 802.11ac (rtl8812au)

This is a re-fork of the Realtek 802.11ac (rtl8812au) v4.2.2 (7502.20130507) driver altered to build on Linux kernel version >= 3.10.

### Purpose

My TP-Link Archer T4U wireless dual-band USB adapter needs the Realtek 8812au driver to work under Linux.

The current rtl8812au version (per nov. 20th 2013) doesn't compile on Linux kernels >= 3.10 due to a change in the proc entry API, specifically the deprecation of the `create_proc_entry()` and `create_proc_read_entry()` functions in favor of the new `proc_create()` function.

### Building (RPI by default)

The Makefile is preconfigured to handle the Raspberry Pi. You may need to modify KSRC to your settings, but in most cases it will be fine. If you are compiling for other architecture, you need to first select the platform.

The driver is built by running `make`, and can be tested by loading the built module using `insmod`:

```sh
$ make
$ sudo insmod 8812au.ko
```

After loading the module, a wireless network interface named __Realtek 802.11n WLAN Adapter__ should be available.

### Installing

Installing the driver is simply a matter of copying the built module into the correct location and updating module dependencies using `depmod`:

```sh
$ sudo cp 8812au.ko /lib/modules/$(uname -r)/kernel/drivers/net/wireless
$ sudo depmod
```

The driver module should now be loaded automatically.

### References

- D-Link DWA-171
  - [D-Link page](http://www.dlink.com/no/nb/home-solutions/connect/adapters/dwa-171-wireless-ac-dual-band-usb-adapter)
  - [wikidevi page](http://wikidevi.com/wiki/D-Link_DWA-171_rev_A1)
