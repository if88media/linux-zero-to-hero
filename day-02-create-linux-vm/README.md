# Day 02 — Install Rocky Linux on VMware

[Back to course](../README.md) · [Next: First commands](../day-03-first-commands/README.md)

## Goal
Build a Linux VM, log in, update its packages, and save a clean recovery point.

## The four resources

| Resource | Purpose | Course VM allocation |
| --- | --- | --- |
| CPU | Executes instructions | 2 virtual CPUs |
| RAM | Holds active program data | 4 GB for Minimal Install |
| Disk | Stores files persistently | 250 GB virtual disk; verify actual capacity in installer |
| Network | Connects systems and repositories | NAT |

An 8 GB RAM host can start with one 4 GB VM; close unnecessary applications.
A growing virtual disk consumes host storage as data is written. Allow extra space for snapshots.
The host's total disk capacity is not its free space.

## Installation checklist

1. Create a VM named `linux-node1` and attach the verified Rocky Linux ISO.
2. Set the resources above and use UEFI firmware.
3. Boot the installer; choose language, keyboard, time zone, and **Minimal Install**.
4. Enable networking and set hostname `linux-node1`.
5. Create `admin88` and select **Make this user administrator**.
6. Select only this new VM's empty disk for installation.
7. Configure custom storage and review all pending changes before accepting them.

## Storage plan

| Mount point / area | Allocation | Purpose |
| --- | --- | --- |
| `/` | 100 GiB | Root filesystem: system files and applications |
| `/var` | 80 GiB | Logs, caches, and changing service data |
| `/home` | 60 GiB | Ordinary users' personal files |
| `/boot` | 2 GiB | Kernel and boot files |
| `/boot/efi` | 600 MiB | UEFI boot files |
| Swap | 4 GiB | Disk-backed support for memory management |

Use LVM and XFS for `/`, `/var`, and `/home`. Keep `/boot` and the EFI partition separate;
use the installer's appropriate EFI filesystem. These are teaching allocations, not OS minima.

The plan needs about **246.6 GiB**. GB and GiB differ: if the installer exposes less space,
enlarge the empty VM disk before installation or reduce the allocations. Leave remaining space available.
The root filesystem `/` is different from the root user's home directory `/root`.

## First login and update

Finish installation and reboot. Disconnect the ISO if the installer starts again.
Log in as `admin88`, then run:

```bash
sudo dnf update -y
```

`sudo` requests administrative privileges; `dnf` manages packages; `update` updates installed
packages; `-y` answers yes to confirmation prompts. Wait for successful completion.
If it fails, inspect the error and network connection before proceeding.

```bash
sudo reboot
```

After logging in again:

```bash
cat /etc/os-release
uname -r
df -h
```

Confirm Rocky Linux, the running kernel, and your mounted filesystems.
Shut down cleanly with `sudo poweroff`, then create a VMware snapshot named
`day02-installed-updated`. A snapshot is a lab recovery point, not an independent backup.

## Your practice task
Start the VM again, log in, and identify `/`, `/var`, and `/home` in `df -h`.

## Reference and video

- [Official installation guide](https://docs.rockylinux.org/guides/installation/)
- Video: https://www.youtube.com/watch?v=x__Ut1lO5Yk

