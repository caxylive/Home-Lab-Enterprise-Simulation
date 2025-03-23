<a name="top"></a>
[Back to Main](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/blob/main/README.md)

---

# Steps to Use USB Passthrough with USB/IP

---

## 1.) Install USB/IP on the client (I'm using Linux Client):

* Since the USB device is physically connected the the client (my Linux laptop), this machine acts as the USB server.


* Install USB/IP:


* Identify the connected USB device:


* Bind the USB device to make it shareable:


* Replace `<BUS-ID>` with the USB device ID you identified earlier.

[Back to Top](#top)

---

# 2.) Install USB/IP on the Proxox Host:

* The Proxmox host will act as the USB client, receiving the shared USB device over the network.
* Install the USB/IP tools:
* Attach the shared USB device from the client:
* Replace `<IP-ADDRESS>` with your client's local IP address and `<BUS-ID>` with the device ID.

[Back to Top](#top)

---

# 3.) Add the USB Device to Your VM:

* Once the Proxmox host detects the USB device, open the Proxmox Web Interface.
* Navigate to the VM (in my case, VM 100 Windows Server 2022).
* Go the the Hadware tab and add the detected USB device to the VM.
* Boot the VM and check if the USB device is available on Windows Server (or your target VM).

[Back to Top](#top)

---

This setup ensures that the USB device connected to client is shared via the Proxmox host and passed into your VM.

[Back to Top](#top)
