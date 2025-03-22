<a name="top"></a>
[Back to Main](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/blob/main/README.md)

---

## Check Network Interface Support:

* Open the Proxmox terminal and run:
  ```Bash
  ethtool <interface_name>
  ```

* Look for a line like `Supports Wake-on: g`.
* If it says `g`, your network card supports WoL.

[Back to Top](#top)

---

## Enable WoL on the Network Interface (Non-Persistent):

* Even if the BIOS doesn't show a WoL option, the network card might still support it.

* The `ethtool` command allows to check and enable WoL:
  ```Bash
  ethtool -s <interface_name> wol g
  ```

* Replace `<interface_name>` with your network interface

* This enables WoL using "magic packets".

[Back to Top](#top)

---

## Make the WoL Persistent:

* Edit the network configuration file:
  ```Bash
  nano /etc/network/interfaces
  ```

* Add the following lines under your network interface configuration:
  ```Bash
  post-up ethtool -s enx00e04c36001d wol g
  ```

* Find the configuration for `vmbr0` and its physical interface. It should something like this:
  ```Bash
  auto enx00e04c36001d
  iface enx00e04c36001d inet manual
      post-up ethtool -s enx00e04c36001d wol g
  ```
* Edit the `/etc/network/interfaces` to look something like this:

  ```
  auto lo
  iface lo inet loopback

  # Physical interface
  auto enx00e04c36001d
  iface enx00e04c36001d inet manual
      post-up ethtool -s enx00e04c36001d wol g

  # Bridge interface for VMs/containers
  auto vmbr0
  iface vmbr0 inet static
      address 10.118.1.254/24
      gateway 10.118.1.1
      bridge-ports enx00e04c36001d
      bridge-stp off
      bridge-fd 0

  # Wireless interface (manual, no IP config for now)
  iface wlp0s20f3 inet manual

  # Source additional configurations
  source /etc/network/interfaces.d/*
  ```

* Save and exit the file.

* Restart the networking service to apply changes:
  ```Bash
  systemctl restart networking
  ```

[Back to Top](#top)

---

## Retrieve the MAC Address
* Run:
```Bash
ip addr
```

* Note the MAC address of your network interface.

[Back to Top](#top)

---

## Send a Magic Packet:

Let's use a tool to send a magic packet to the server's MAC Address:

  * Windows PowerShell:
    ```Powershell
    $mac = "00:e0:4c:36:00:1d"
    $packet = [byte[]](,0xFF * 102)
    6..101 | ForEach-Object { $packet[$_] = [byte[]]::Parse($mac.Replace(":", "").Substring(($_ % 6) * 2, 2), "X2") }
    $client = New-Object System.Net.Sockets.UdpClient
    $client.Connect("255.255.255.255", 9)
    $client.Send($packet, $packet.Length)
    $client.Close()
    ```
    * `00:e0:4c:36:00:1d` is my USB RJ45's MAC Address. Replace it with the MAC Address of your interface.

  * Linux / macOS:
    ```Bash
    sudo apt install wakeonlan
    wakeonlan -i 10.118.1.255 00:e0:4c:36:00:1d
    ```

    * Replace the Broadcast Address and MAC Address accordingly.

  * Android / iOS:
    * Use an app like `Wake On LAN`

---

## What is a Bridge?

In networking, a bridge (like `vmbr0` in my setup) is used to connect multiple network interfaces and allow communication between them. In the context of Proxmox:

  * A bridge acts like a virtual switch, connecting my physical network interface (e.g., `enx00e04c36001d`) to my virtual machines.

  * It enables virtual machines to share the same network as the Proxmox host, giving each VM its own IP address that’s accessible on the network.

In simple terms, `vmbr0` is the bridge that links my laptop's physical Ethernet connection (`enx00e04c36001d`) to the VMs I’ll run in Proxmox, so everything communicates seamlessly on my home network.

---

## Ensuring USB Ethernet Interface Remains Powered during Shutdown:

### 1. Check USB Power Management USettings

1. Open the terminal and edit the USB power settings:
2. Add the following parameter to the `GRUB_CMDLINE_LINUX_DEFAULT` line:
3. Save and exit.
4. Update GRUB to apply the changes:
5. Reboot the system to ensure the changes take effect.

### 2. Enable USB Wake Support
Check if the USB Ethernet interface supports wake events:
1. List all USB devices:
2. Identify the USB Ethernet adapter and note the bus and device ID.
3. Enable wake events for the device:

### 3. Test USB Power During Shutdown
After applying the above settings, shut down the Proxmox Machine and check if the USB Ethernet adapter remains powered (e.g., by observing its activity lights).

### 4. BIOS/UEFI Settings
Whenever possible, try disabling `Fast Boot` or similar feature to ensure USB ports remain powered.

[Back to Top](#top)

--- 
