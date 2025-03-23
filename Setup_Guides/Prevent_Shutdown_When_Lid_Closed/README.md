<a name="top"></a>
[Back to Main](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/blob/main/README.md)

# Configuring logind.conf to Prevent Shutdown When Lid is Closed

---

Author: Carl Xymon Verdejo

Contact: carl.xymon.verdejo@gmail.com

--- 

## Introduction

This guide explains how to modify the logind.conf file in a Linux-based system to ensure that the machine stays active and does not suspend when the laptop lid is closed. This can be especially useful for systems running Proxmox or similar server setups.
Steps

[Back to Top](#top)

---

### 1. Locate the `logind.conf` File

The file is located in:
```
/etc/systemd/logind.conf
```

---

### 2. Edit the Configuration

Open the file for editing:
```Bash
nano /etc/systemd/logind.conf
```

Look for the following lines in the `[Login]` section:
```Paintext
#HandleLidSwitch=suspend
#HandleLidSwitchExternalPower=suspend
#HandleLidSwitchDocked=ignore
```

Uncomment and modify them as follows:
```Plaintext
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```

This configuration ensures the system will ignore the lid-close event under all power conditions.

---

### 3. Apply the Changes

After saving the file (CTRL+O, then CTRL+X to exit nano), restart the systemd-logind service to apply the changes:
```bash
systemctl restart systemd.logind.service
```

---

### 4. Test the Configuration

Close the lid of the laptop and verify that the machine continues to run (e.g., the Proxmox web interface should remain accessible).

[Back to Top](#top)

---

## Verification

* Ensure the changes are applied by running:
  ```Bash
  systemctl status systemd-logind
  ```

* Verify that no lid-close events trigger a suspension.

[Back to Top](#top)

---

## Notes

* If this file or configuration gets reset during an update, the steps above can be repeated.
* For more details, refer to the `login.conf` manual page:
  ```Bash
  man logind.conf
  ```

[Back to Top](#top)

---
