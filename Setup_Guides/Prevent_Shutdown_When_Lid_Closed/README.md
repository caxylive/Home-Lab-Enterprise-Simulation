<a name="top"></a>
[Back to Main](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/tree/main)
# Configuring logind.conf to Prevent Shutdown When Lid is Closed

---

Author: Carl Xymon Verdejo

Contact: carl.xymon.verdejo@gmail.com

--- 

## Introduction

This guide explains how to modify the logind.conf file in a Linux-based system to ensure that the machine stays active and does not suspend when the laptop lid is closed. This can be especially useful for systems running Proxmox or similar server setups.
Steps
1. Locate the `logind.conf` File

The file is located in:
```
/etc/systemd/logind.conf
```
