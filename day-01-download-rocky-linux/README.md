# Day 01 — Download Rocky Linux

[Back to course](../README.md) · [Next: Install Rocky Linux](../day-02-install-rocky/README.md)

## Goal
Download the Rocky Linux installation image for our next lesson.

## Before you start
Complete Day 00. Our main course uses Rocky Linux 10 on a compatible Intel/AMD x86-64 host.
Rocky Linux 10 requires x86-64-v3 support on this architecture.
See the official [hardware requirements](https://docs.rockylinux.org/guides/minimum_hardware_requirements/).

## Walkthrough

1. Open the official [Rocky Linux downloads](https://rockylinux.org/download).
2. Select the current Rocky Linux 10 release and the architecture matching your compatible host.
3. Use the DVD ISO for this walkthrough so installation content is available locally.
4. Save the ISO in a folder you can find easily.
5. Verify its SHA-256 checksum against the official checksum for that exact image.

An ISO is installation media. Downloading it does not install Linux.

On your Windows host, run this in PowerShell, replacing the filename:

```powershell
Get-FileHash -Algorithm SHA256 .\YOUR-ROCKY-IMAGE.iso
```

Compare the entire hash with the official value for the same filename.
If they differ, do not use the image; confirm the filename and obtain a valid copy.

## Your practice task
Locate your ISO and record its release, architecture, filename, and checksum result.
Installation is Day 02.

## Video
Link: https://www.youtube.com/watch?v=hhrioBMzbI0&t=18s

