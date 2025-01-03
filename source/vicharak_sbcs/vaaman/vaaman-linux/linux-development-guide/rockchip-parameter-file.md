---
orphan: true
---

# Rockchip Parameter File

## Introduction to the parameter file

The firmware partition information, which is crucial, can be found in the `parameter.txt` file.
Within the device/rockchip/rk3399 directory, you can locate several `parameter.txt` files.

To illustrate, here is an example of the contents of a `parameter.txt` file.

:::{card} device/rockchip/rk3399/parameter-rk3399-ubuntu.txt

```text
FIRMWARE_VER: 8.1
MACHINE_MODEL: RK3399
MACHINE_ID: 007
MANUFACTURER: RK3399
MAGIC: 0x5041524B
ATAG: 0x00200800
MACHINE: 3399
CHECK_MASK: 0x80
PWR_HLD: 0,0,A,0,1
TYPE: GPT
CMDLINE: mtdparts=rk29xxnand:0x00002000@0x00004000(uboot),0x00002000@0x00006000(trust),0x00002000@0x00008000(misc),0x00020000@0x0000a000(boot:bootable),0x00010000@0x0002a000(recovery),0x00010000@0x0003a000(backup),0x00080000@0x0004a000(userdata),-@0x000ca000(rootfs:grow)
uuid:rootfs=614e0000-0000-4b53-8000-1d28000054a9
```

:::

The `CMDLINE` property is of particular importance. Taking uboot as an example, in the format `0x00002000@0x00004000(uboot)`,
the starting position of the uboot partition is `0x00004000`, and the size of the partition is `0x00002000`.

The same partition rules apply to other partitions as well.
Users have the flexibility to add, remove, or modify partition information according to their requirements.
However, it is essential to maintain at least the **uboot, trust, boot, and rootfs** partitions,
as they are necessary for the proper functioning of the device.

The `parameter-ubuntu.txt` file follows a simple partition scheme.

### Brief introduction to each partition

#### uboot

This partition is used to upgrade the uboot.img compiled by uboot.

#### trust

This partition is used to upgrade the trust.img compiled by uboot.

#### misc

This partition is used to upgrade the misc.img and facilitates entering recovery mode (details omitted).

#### boot

This partition is used to upgrade the boot.img compiled by the kernel and contains kernel and device tree information.

#### recovery

This partition is used to upgrade the recovery.img (details omitted).

#### backup

This partition is currently reserved and not in use.
It may be used in the future as a backup for recovery, similar to Android (details omitted).

#### rootfs

This partition stores the rootfs.img compiled by Buildroot, Debian or Ubuntu rootfs and is read-only.

#### userdata

This partition is used to store files generated by the app or for end-users.
It is read and write accessible and mounted at `/userdata` (details omitted).
