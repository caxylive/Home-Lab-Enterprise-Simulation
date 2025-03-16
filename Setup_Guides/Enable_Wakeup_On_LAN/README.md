<a name="top"></a>
[Back to Main](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/blob/main/README.md)

---

## Check Network Interface Support

* Open the Proxmox shell and run:
  ```Bash
  ethtool <interface_name>
  ```
  Look for a line like `Supports Wake-on: g`. If it says `g`, your network card supports WoL.

[Back to Top](#top)

---

## Enable WoL on the Network Interface (non-persistent)

* Even if the BIOS doesn't show a WoL option, the network card might still support it. The `ethtool` command allows to check and enable WoL:
  ```Bash
  ethtool -s <interface_name> wol g
  ```
  Replace `<interface_name>` with your network interface
* This enables WoL using "magic packets".

[Back to Top](#top)

---

## Make the WoL Persistent

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

## Send a Magic Packet

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
    * Take note of the broadcast address and MAC Address. 

  * Android / iOS:
    * Use an app like `Wake On LAN`

---

## What is a Bridge?

In networking, a bridge (like `vmbr0` in my setup) is used to connect multiple network interfaces and allow communication between them. In the context of Proxmox:

  * A bridge acts like a virtual switch, connecting my physical network interface (e.g., `enx00e04c36001d`) to my virtual machines.

  * It enables virtual machines to share the same network as the Proxmox host, giving each VM its own IP address that’s accessible on the network.

In simple terms, `vmbr0` is the bridge that links my laptop's physical Ethernet connection (`enx00e04c36001d`) to the VMs I’ll run in Proxmox, so everything communicates seamlessly on my home network.
