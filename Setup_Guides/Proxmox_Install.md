# Proxmox Installation Guide

## Overview
Proxmox Virtual Environment (Proxmox VE) is an open-source server virtualization platform that allows you to create and manage virtual machines and containers efficiently. This guide outlines the steps to install Proxmox VE on your system, configure basic settings, and prepare it for hosting virtual machines.

## Prerequisites
### **Hardware**
- **Laptop:** Repurposed laptop with Intel Core i7-1260P, 16GB DDR5 RAM, 2x 1TB SSDs
- **Bootable USB Drive:** At least 8GB (Ventoy recommended)
- **Internet Connection:** Required for updates and package installations

### **Software Requirements**
- **Proxmox VE ISO** (Downloaded)
- **Ventoy** (For creating a bootable USB drive)
- **Backup Software:** Clonezilla, Acronis, or another backup tool (optional but recommended)

## Step 1: Backup Important Data
Before proceeding, back up all important files to external storage (SSD, USB drive, or cloud storage). If you plan to dual-boot with Windows, consider creating a full system image using Clonezilla or Acronis.

## Step 2: Create a Bootable USB Drive with Ventoy
1. Insert the USB drive into your computer.
2. Open **Ventoy** and format the USB drive.
3. Copy the **Proxmox VE ISO** onto the Ventoy USB.
4. Ensure the ISO is properly copied by listing the files in the USB drive.

## Step 3: Configure BIOS Settings
1. Restart your laptop and enter BIOS (**F2, F12, DEL, or ESC**, depending on your system).
2. Enable **Virtualization Technology (VT-x / AMD-V)**.
3. Disable **Secure Boot** to allow unsigned OS installations.
4. Set the **Boot Order** to prioritize USB first.
5. Save and exit.

## Step 4: Install Proxmox VE
1. Boot from the **Ventoy USB** containing the Proxmox ISO.
2. Select **Install Proxmox VE** from the menu.
3. Accept the End User License Agreement (EULA).
4. Choose the installation target (your main SSD, e.g., `/dev/nvme0n1`).
5. Select the filesystem type (**ext4** or **ZFS** for RAID setups).
6. Configure basic settings:
   - **Country, Timezone, and Keyboard Layout**
   - **Admin Password and Email Address**
7. Configure networking:
   - Assign a **static IP address** (recommended)
   - Set **Gateway and DNS** values
8. Confirm settings and start the installation.

## Step 5: First Boot and Web GUI Access
1. After installation, remove the USB drive and reboot.
2. Once Proxmox boots, access the web GUI using:
   ```
   https://<your-server-ip>:8006
   ```
3. Log in using the `root` account and the password you set during installation.

## Step 6: Post-Installation Configuration
### **Update and Enable Non-Subscription Repositories**
Proxmox comes with a subscription-based enterprise repository. To use the community repository instead:
1. Open the Proxmox terminal or SSH into the server.
2. Edit the repository list:
   ```bash
   nano /etc/apt/sources.list.d/pve-enterprise.list
   ```
3. Comment out the enterprise repo:
   ```bash
   #deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
   ```
4. Add the community repository:
   ```bash
   echo "deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription" | sudo tee /etc/apt/sources.list.d/pve-community.list
   ```
5. Update the system:
   ```bash
   apt update && apt full-upgrade -y
   ```

## Step 7: Configure Storage
- Add additional disks (if available) for VM storage.
- Set up a **ZFS pool** if using multiple drives.
- Configure **LVM storage** for better performance.

## Step 8: Network Configuration
- Set up **bridged networking** for VMs to connect to the local network.
- Configure **VLANs** if you plan to simulate an enterprise environment.

## Step 9: Create Your First VM
1. Go to the **Proxmox Web GUI**.
2. Click **Create VM**.
3. Select an ISO (Ubuntu, Windows Server, Kali Linux, etc.).
4. Assign CPU, RAM, and disk resources.
5. Complete the setup and boot the VM.

## Troubleshooting
- **Can't access Proxmox Web GUI?** Ensure the correct IP is set and Proxmox services are running.
- **Networking issues?** Check firewall rules and bridges.
- **Proxmox updates failing?** Verify repository configuration.

## Next Steps
- Install **pfSense** for firewall & network security.
- Set up Windows Server roles (Active Directory, DNS, DHCP, File Server, etc.).
- Create VMs for cybersecurity tools (Kali Linux, Metasploitable, Wazuh, Suricata).

---
🚀 **This guide will be continuously updated as the home lab evolves. Stay tuned!**

