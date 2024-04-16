---
title: "Testing New LibreMesh Release"
date: 2024-02-15
description: "A documentation about the tests of the new version of LibreMesh on New Hardware Reporting."
image: "/images/libremesh.png"
type: "post"
tags: ["RedesComunitarias","libremesh"]
---

### Motivation

Testing routers with the latest version of LibreMesh is crucial for community networks that rely on mesh networks as their communication infrastructure. The significance lies in the fact that insufficient testing hinders the development of newer versions. Currently, the official version of LibreMesh is tied to the 2019 release of OpenWRT. This limitation impedes progress, as advancements and improvements are often left unexplored. By conducting thorough tests with the most recent version, we pave the way for enhanced features, increased stability, and better overall performance. It is through these tests that we identify and address potential issues, ensuring a robust and reliable platform for community networks. Moving beyond the 2019 OpenWRT version opens up opportunities for innovation and keeps LibreMesh at the forefront of mesh networking technology. Therefore, a concerted effort in testing is essential to drive the evolution of LibreMesh and contribute to the continued growth of community-driven, mesh-based communication networks.#

https://downloads.libremesh.org/development/master-ow23.05.0/

### Devices tested

#### Eap225-outdoor v3

![](https://static.tp-link.com/upload/image-line/EAP225-Outdoor_normal_20230821083554a.png)

Certainly! Here's the corrected text:

Testing the TP-Link EAP225-Outdoor V3 router is motivated by the increasing demand for robust wireless solutions in community networks, particularly in outdoor settings like parks. The motivation stems from the desire to address the unique challenges posed by external environments and accommodate a high volume of users simultaneously. The EAP225-Outdoor V3 presents itself as a potential solution, designed to provide reliable Wi-Fi connectivity in outdoor spaces with a focus on scalability and performance. Notably, it stands out as the most cost-effective option in its category, making it an attractive choice for community networks with budget constraints. Testing this router in such community network scenarios becomes essential to ensure its compatibility with outdoor conditions and its ability to handle the expected user load effectively. By conducting thorough tests, network administrators can ascertain the EAP225-Outdoor V3's suitability for community-driven outdoor areas, contributing to the creation of accessible and reliable wireless networks in public spaces.

This equipment had a relatively simple process to install LibreMesh. Following the documentation provided by OpenWrt, the system worked normally.

Steps

1 - Power on and set your IP to 192.168.0.1 and the gateway to 192.168.0.254.
2 - Log in to the web page and enable SSH access, then log in using SSH.
3 - SSH into the router (ssh user@192.168.0.254) and run `cliclientd stopcs`.
4 - Upload the firmware with a short name (less than 63 characters).

The router then joined the available mesh in the community with an older Lime version.

Problems

1 - `thisnode.info` is not working due to an SSL problem; sometimes we need to explicitly use HTTP.
2 - The firstboot wizard is not working.
3 - Remote support is not functioning, returning "Please check that the `ubus-tmate` package is installed."
4 - Voucher access is not working; in the browser console, it returns "Uncaught (in promise) TypeError: Cannot read properties of null (reading 'sort')."


- Oficial Page - https://www.tp-link.com/us/business-networking/ceiling-mount-access-point/eap225-outdoor/

- Ref. https://openwrt.org/toh/tp-link/eap225 

### CPE510 v3

![](https://openwrt.org/_media/media/tplink/cpe210.png)

Testing the TP-Link EAP225-Outdoor V3 router is motivated by the increasing demand for robust wireless solutions in community networks, particularly in outdoor settings like parks. The motivation stems from the desire to address the unique challenges posed by external environments and accommodate a high volume of users simultaneously. The EAP225-Outdoor V3 presents itself as a potential solution, designed to provide reliable Wi-Fi connectivity in outdoor spaces with a focus on scalability and performance. Notably, it stands out as the most cost-effective option in its category, making it an attractive choice for community networks with budget constraints. Testing this router in such community network scenarios becomes essential to ensure its compatibility with outdoor conditions and its ability to handle the expected user load effectively. By conducting thorough tests, network administrators can ascertain the EAP225-Outdoor V3's suitability for community-driven outdoor areas, contributing to the creation of accessible and reliable wireless networks in public spaces.

This equipment had a relatively simple process to install LibreMesh. Following the documentation provided by OpenWrt, the system worked normally.

Steps

1 - Power on and set your IP to 192.168.0.1 and the gateway to 192.168.0.254.
2 - Log in to the web page and enable SSH access, then log in using SSH.
3 - SSH into the router (ssh user@192.168.0.254) and run cliclientd stopcs.
4 - Upload the firmware with a short name (less than 63 characters).

The router then joined the available mesh in the community with an older Lime version.

Problems

1 - thisnode.info is not working due to an SSL problem; sometimes we need to explicitly use HTTP.
2 - The firstboot wizard is not working.
3 - Remote support is not functioning, returning "Please check that the ubus-tmate package is installed."
4 - Voucher access is not working; in the browser console, it returns "Uncaught (in promise) TypeError: Cannot read properties of null (reading 'sort')."

Despite the problems encountered, this router has worked very well on the libremesh roadmap and these problems have already been addressed and we should soon have a well-rounded system.

- Oficial page - https://www.tp-link.com/en/business-networking/outdoor-radio/cpe510/v3/

- Ref.
    1 - https://openwrt.org/toh/tp-link/cpe510


#### Archer AX23 v1 

![](https://openwrt.org/_media/media/tplink/archer_ax23.jpeg?w=500&tok=252bd5)

With the old versions of LibreMesh, a widely used router that is almost no longer on the market is the TP-Link Archer C7, and a good replacement for it could be the Archer AX23. When comparing the Archer C7 with the more recent Archer AX23, it becomes evident that the AX23 represents a significant advancement in networking technology. While the Archer C7 V1 has been a reliable choice for community networks, the AX23 outshines it in various aspects. The Archer AX23 introduces Wi-Fi 6 technology, delivering notably faster speeds and improved overall network performance compared to the older Wi-Fi 5 standard utilized by the Archer C7 V1. With features like increased capacity and improved efficiency in handling multiple devices concurrently, the AX23 addresses the escalating connectivity needs of contemporary community networks. Furthermore, the AX23 incorporates advanced technologies such as MU-MIMO and Beamforming, contributing to a more stable and efficient wireless connection. As community networks evolve, the Archer AX23 emerges as a superior and future-ready solution, offering enhanced capabilities to meet the demands of the ever-changing digital landscape.

1 - Log into the TP-Link system > upload firmware.
2 - Choose the firmware.

After rebooting, the router works with LibreMesh, but for some reason, the system did not come with the correct IP range as expected. I tried to use sysupgrade firmware, and the router broke. To recover, hold the reset button while powering on the router, and release the reset button when only the orange WAN LED is on, then upload the TP-Link factory firmware.


- Oficial Page - https://www.tp-link.com/my/home-networking/wifi-router/archer-ax23/

- Ref. 
        1 - https://openwrt.org/toh/tp-link/archer_ax23_v1
        2 - https://forum.openwrt.org/t/add-support-for-tp-link-ax23-v1/130746/55?page=2

#### Nanostation Ac Loco (airOs v8.7.9)

![](https://openwrt.org/_media/media/ubiquiti/nanostation_ac_back.jpg?cache=&w=334&h=600&tok=1c5527)

Because it has two 5.8GHz radios, this equipment is very interesting for use in community networks. We can use one radio for mesh and the other to connect to clients, which is crucial for establishing a more stable mesh network, avoiding issues such as the [Hidden node problem](https://en.wikipedia.org/wiki/Hidden_node_problem). 

In this case, the router was initially equipped with Ubiquiti's airOS version 8.7.9. However, I needed to downgrade it to version 8.7.0. Unfortunately, the system was restricted and did not allow the installation of older firmware versions.

What has made this equipment more challenging is a problem that even the OpenWrt community hasn't been able to solve yet, as described [in this post](https://forum.openwrt.org/t/installing-openwrt-on-nanostation-5ac-loco/71035)



**Hypotheses investigated**

1 - Removing part of the firmware upgrade program that checks the version of the candidate file for an upgrade, as described in the [common procedures for uniquitis](https://openwrt.org/toh/ubiquiti/common)

With access to the SSH terminal, I attempted to create a new upgrade file.

```
WA# hexdump -Cv /bin/ubntbox | sed 's/14 40 fe fe/00 00 00 00/g' | hexdump -R > /tmp/fwupdate.real
WA# chmod +x /tmp/fwupdate.real 
WA# /tmp/fwupdate.real -m WA.v8.7.0.42152.200203.1256.bin 
Invalid version 'WA.ar934x.v8.7.0.42152.200203.1256'
```
but it didn't work.

2 - Use the binary from the version update program that accepts updates:

Since it is not possible to downgrade the system, the attempt was made to extract the binary that checks the update file of the previous version, which is already documented on how to proceed.

So, using the binwalk command, I extracted the binary files from a WA.ar934x.v8.7.0.42152.200203.1256 version of airOS.

```
binwalk -Me WA.v8.7.0.42152.200203.1256.bin

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Ubiquiti firmware header, header size: 264 bytes, ~CRC32: 0x8E4EB358, version: "WA.ar934x.v8.7.0.42152.200203.1256"
268           0x10C           Ubiquiti partition header, header size: 56 bytes, name: "PARTu-boot", base address: 0x9F000000, data size: 231788 bytes
115476        0x1C314         Certificate in DER format (x509 v3), header length: 4, sequence length: 64
143220        0x22F74         U-Boot version string, "U-Boot 1.1.4-s1102 (Mar  5 2019 - 17:13:19)"
143508        0x23094         CRC32 polynomial table, big endian
224688        0x36DB0         CRC32 polynomial table, big endian
232120        0x38AB8         Ubiquiti partition header, header size: 56 bytes, name: "PARTkernel", base address: 0x9F050000, data size: 991878 bytes
232176        0x38AF0         uImage header, header size: 64 bytes, header CRC: 0xA68651F0, created: 2020-02-03 11:03:06, image size: 991814 bytes, Data Address: 0x80002000, Entry Point: 0x80002000, data CRC: 0x6458CA58, OS: Linux, CPU: MIPS, image type: OS Kernel Image, compression type: lzma, image name: "MIPS Ubiquiti Linux-2.6.32.68"
232240        0x38B30         LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 2844788 bytes
1224062       0x12AD7E        Ubiquiti partition header, header size: 56 bytes, name: "PARTrootfs", base address: 0x9F150000, data size: 7995392 bytes
1224118       0x12ADB6        Squashfs filesystem, little endian, version 4.0, compression:lzma, size: 7675509 bytes, 988 inodes, blocksize: 262144 bytes, created: 2020-02-03 11:03:08
9219518       0x8CADBE        Ubiquiti firmware additional data, name: script, size: 398 bytes, size2: 398 bytes, CRC32: 8fdcf4e2
9219574       0x8CADF6        gzip compressed data, from Unix, last modified: 2020-02-03 11:01:05
9219980       0x8CAF8C        Signed Ubiquiti end header, RSA 2048 bit, header size: 264 bytes


```


So in the binaries folder, I found the file ubntbox, which serves as the target for the symbolic link directed from the file fwupdate.real. Copying this binary to the router, I got the following output:

```
WA# /tmp/fwupdate.real -m openwrt-ubnt_initramfs.bin 
/tmp/fwupdate.real: can't load library 'libssl.so.1.0.0'
```
In other words, we need a library for this binary to work since this library has been updated in the new version. I also tried to create a symbolic link from the newer library to this one, but it wasn't possible to create a symbolic link because the system is set to read-only.

```
WA# ln -s /lib/libssl.so.1.1 /lib/libssl.so.1.0.0
ln: /lib/libssl.so.1.0.0: Read-only file system
```

3 - Accessing u-boot and loading firmware into flash

To access u-boot, I had to connect it via a serial port. To do this, I had to solder a flash-serial adapter to the router's circuitry and make a USB connection to the computer to access the router's u-boot.

![](https://md.coolab.org/uploads/upload_1d1e3f638320c6fb7441a1be27dfa3f1.jpg)


As soon as the system starts booting, we get a message saying Hit any key to stop autoboot: 0. Pressing Enter at this point stops the system from booting.

```
U-Boot 1.1.4-s1102 (Mar  5 2019 - 17:13:19)

DRAM:  64 MB
Flash: 16 MB (0xc2, 0x20, 0x18)
PCIe WLAN Module found (#1).
Net:   AR8035
eth0, eth1
Board: Ubiquiti Networks AR9342 board (e7fa-141334.1123.0030.0031)
Radio: 0777:e7fa
Reset: Normal
Hit any key to stop autoboot:  0 
ar7240> 
ar7240> 
ar7240> 
```
Now that you have access to the terminal, you can start the boot process using tftpboot.

```
ar7240> tftpboot
*** Warning: no boot file name; using '1401A8C0.img'
Using eth0 device
TFTP from server 192.168.1.254; our IP address is 192.168.1.20
Filename '1401A8C0.img'.
Load address: 0x81000000
Loading: T T T T 
Retry count exceeded; starting again
Invalid speed detected
*** Warning: no boot file name; using '1401A8C0.img'

```
Simultaneously, on one computer, you need to create a TFTP server with a fixed IP at 192.168.1.254 and serving a file called 1401A8C0.img. This file must be an initramfs image of OpenWrt, in this case, LibreMesh.

Once the file has been sent, boot the system with bootm. Once the system has booted, you have access to a terminal inside OpenWrt to perform the final upgrade.

```
root@OpenWrt:/tmp# mtd -r write /tmp/libremesh-master-ow23.05.2-default-ath79-generic-ubnt_nanostation-ac-loco-squashfs-sysupgrade.bin firmware
Unlocking firmware ...

Writing from /tmp/libremesh-master-ow23.05.2-default-ath79-generic-ubnt_nanostation-ac-loco-squashfs-sysupgrade.bin to firmware .

```

The system didn't work exactly as expected, but it is running with LibreMesh. In the end, when the radio is accessed, the router crashes and throws this message on the serial:

```
[  170.973497] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  170.981767] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  170.989976] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  170.998244] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  171.006297] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  171.014288] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  171.022518] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  171.030505] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  171.038691] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  171.046727] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098
[  171.060059] jffs2: Node CRC ffffffff != calculated CRC f09e7845 for node at 007e5098

```


- Oficial Page - https://store.ui.com/us/en/products/loco5ac

- Datasheet - https://dl.ubnt.com/datasheets/NanoStation_AC/NanoStation_AC_DS.pdf

- Ref. 
    1 - https://openwrt.org/toh/ubiquiti/nanostation_ac_loco
    2 - https://openwrt.org/toh/ubiquiti/common
    3 - https://ui.com/download/airmax-ac
    4 - https://massmesh.org/wiki/index.php?title=Ubiquiti_NanoStation_5AC_Loco
    5 - https://forum.openwrt.org/t/install-openwrt-on-an-ubiquiti-nanostation-ac-loco/53574
    6 - https://forum.openwrt.org/t/installing-openwrt-on-nanostation-5ac-loco/71035


### Conclusion

The Tplink eap225 outdoor v3 and the cpe510 v3 worked superbly, some problems related to some open issues in the libremesh project are already in sight to be fixed and should be great options for community networks in 2024.
The loco ac Loco (and similar) and ax23 should be options soon once we've found the problems with these errors. It doesn't seem to be that difficult once the firmware has been written to the router's memory and it has completed the boot process.
The errors found will be reported and some work will still be needed to resolve them.

