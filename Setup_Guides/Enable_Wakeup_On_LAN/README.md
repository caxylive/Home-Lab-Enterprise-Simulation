---

## Check USB Power Management Settings

Linux systems often manage USB power through the `autosuspend` feature. You can disable it to ensure the USB interface remains active:

1. Open the terminal and edit the USB power settings:
  ```Bash
  nano /etc/default/grub
  ```

2. Add the following parameter to the `GRUB_CMDLINE_LINUX_DEFAULT` line:
  ```
  usbcore.autosuspend=-1
  ```

  For example:
  ```
  GRUB_CMDLINE_LINUX_DEFAULT="quiet splash usbcore.autosuspend=-1"
  ```

3. Save and exit.

4. Update GRUB to apply the changes:
  ```Bash
  update-grub
  ```

5. Reboot the system to ensure the changes take effect.

[Back to Top](#top)

---

## Disable USB Autosuspend

1. Open the GRUB configuration:
   ```Bash
   nano /etc/default/grub
   ```

2. Add the following parameter to the `GRUB_CMDLINE_LINUX_DEFAULT` line:
   ```Bash
   usbcore.autosuspend=-1
   ```

3. Save and exit.

4. Update the GRUB:
   ```Bash
   update-grub
   ```

5. Reboot the system for the system for the changes to take effect:
   ```Bash
   reboot
   ```

6. 

---

## Enable Wakeup for the USB Ethernet Adapter

1. Find the adapter's device path:
  ```Bash
  ls /sys/bus/usb/devices/*/power/wakeup
  ```
  Look for the path corresponding to the Ethernet Adapter (i.e., `Bus 001 Device 005`). It might look something like `/sys/bus/usb/devices/1-5/power/wakeup`.

2. Enable wakeup on the `usb1` device:

3. Verify that the wakeup setting is enabled:
  ```Bash
  cat /sys/bus/usb/devices/usb1/power/wakeup
  ```
  
  It should return `enabled`.
  
---


---

## Test the Configuration

1. Shutdown the Proxmox machine:
2. Try sending the Wake-on-LAN magic packet:
   ```Bash
   wakeonlan <your_usb_rj45_adapter_mac_address>
   ```

---

## Additional Notes

* If `usb1` does ot seem to work, you can also try enabling wakeup for the other candidates (`1-8` or `usb2`).
* To make the wakeup configuration persistent across reboots, you can add the appropriate command to a startup script (e.g., `/etc/rc.local`).

---

 
