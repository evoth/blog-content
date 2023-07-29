---
title: "Android Debug Bridge (ADB)"
date: 2023-07-27T11:26:21-06:00
draft: true
---

Android Debug Bridge (abbreviated as "ADB" or "adb") is a debugging tool that enables communication between Android devices and development machines, either over USB or wirelessly. An ADB client on the development machine connects to a daemon running on the Android device, which exposes a Unix shell and the ability to execute commands on the device. These connections are managed by an ADB server, which also runs on the development machine. To use ADB with a device, the user must allow USB debugging in the developer options.

The `adb` command-line tool invokes the ADB client (starting a server/daemon as needed), supporting common operations such as installing/uninstalling apps, copying files to and from the device, and running shell commands.