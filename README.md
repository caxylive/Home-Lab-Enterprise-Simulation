<a name="top'></a>

# 🏠 Home Lab - Enterprise IT & Cybersecurity Simulation

---

**Author**: [Carl Xymon Verdejo](https://hardworking-lion-z4sd3b.mystrikingly.com/)

**Contact**: carl.xymon.verdejo@gmail.com

---

## 📌 Overview
This project documents my journey in building a **home lab** that simulates a real-world (small-medium business) **enterprise IT environment**. It includes detailed instructions for hardware setup, software installations, network configurations, and hands-on cybersecurity practices. The goal is to gain **hands-on experience** with:
- **System Administration** (Windows Server, Active Directory, DNS, DHCP, File Sharing)
- **Networking** (pfSense Firewall, VPN, GNS3 Network Simulations)
- **Cybersecurity** (SIEM, IDS/IPS, Penetration Testing with Kali Linux & Metasploitable)
- **DevOps & Virtualization** (Proxmox, Docker, Web & Database Servers)

---

## Table of Contents
1. [My Hardware](#my-hardware)
2. [Software Requirements](#software-requirements)
3. [Setup Process and Documentation](#-setup-process-and-documentation)
4. [Lab Infrastructure](#lab-infrastructure)
5. [Future Improvements](#🚀-future-improvements)
6. [Advanced Hands-On Activities](#advanced-hands-on-activities)
7. [Troubleshooting](#troubleshooting)

---

## My Hardware
- **Laptop**
    - PM1: Repurposed laptop with Intel Core i7-1260P, 16GB RAM, and two 1TB SSDs.
    - 
- **Router**: I will **NOT** mention my router brand and model for security reasons (each model has their own unique **vulnerabilities** that hackers can **exploit** to gain access to your system)

- **Cables**: RJ45 (Cat 6a)

- **Peripherals**:
    - USB to Ethernet: to connect machine to router.
    - WiFi Adapter ([TP-Link TL-WN722N](https://www.tp-link.com/ph/home-networking/adapter/tl-wn722n/) supports **monitoring mode** and **packet injection**)

- **Backups**: external storage for backing up important files, ISOs, and software. Please see below for essential ISOs and softwares.

[Back to Top](#top)

---

## Software Requirements
### Essential ISOs
- **[Proxmox VE](https://www.proxmox.com/en/)**: Main hypervisor.
- **Windows Server 2022**: Server roles such as AD, DNS, DHCP.
- **Windows 10/11**: Client OS for testing.
- **[Ubuntu Server](https://ubuntu.com/download/server)**: Web hosting, database servers, security tools.
- **[Kali Linux](https://www.kali.org/)**: Penetration testing.
- **[pfSense](https://www.pfsense.org/)**: Firewall and networking.
- **[Metasploitable](https://github.com/rapid7/metasploitable3/blob/master/README.md)**: Vulnerable VM for pentesting practice.

### Additional ISOs
- **[CentOS](https://www.centos.org/)**
- **[Debian](https://www.debian.org/)**
- **[FreeBSD](https://www.freebsd.org/)**
- **[macOS Catalina](https://archive.org/details/mac-os-catalina-10.15.5-19-f-101_202302)** (For those wanting to try out macOS. Please check hardware compatibility.)

### Essential Software
- **[Ventoy](https://www.ventoy.net/en/index.html)**: Bootable USB creation.
- **[Rufus](https://rufus.ie/en/)**: Bootable USB creation.
- **[PuTTY](https://www.putty.org/)**: SSH and remote management.
- **[WinSCP](https://winscp.net/eng/download.php)**: Secure file transfers.
- **[Visual Studio Code](https://code.visualstudio.com/)**: Scripting and configuration.
- **[Wireshark](https://www.wireshark.org/)**: Network analysis.
- **[Nmap](https://nmap.org/)**: Network scanning.
- **[OpenVPN](https://openvpn.net/)**: VPN testing.
- **[Suricata](https://suricata.io/)**: Intrusion detection and prevention.
- **[Wazuh](https://wazuh.com/)**: SIEM and security monitoring.
- **[GNS3](https://www.gns3.com/)**: Network simulation.
- **[Docker](https://www.docker.com/resources/what-container/)**: Containerized applications.

[Back to Top](#top)

---

## 🔧 Setup Process and Documentation
1. **Backup** files and create **[bootable drives](https://github.com/caxylive/Common-Commands/blob/main/linux%20terminal/bootable_usb.md)** (my tools of choices are **dd**, **Ventoy** and **Rufus**). Refer **[here](https://github.com/caxylive/Common-Commands/blob/main/cmd_scripts/batch_copy_files.bat)** for useful scripts for batch copying files.
2. **[Install Proxmox VE](Setup_Guides/Proxmox_Install.md)** on the host machine.
    a. [Modify logind.conf](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/blob/main/Setup_Guides/Prevent_Shutdown_When_Lid_Closed/README.md) so that the laptop stays powered on even when the lid is shut.
    b. Enable WOL (Wake-On-Lan) to remotely power on machine.
4. **[Create and configure VMs](Setup_Guides/VM_Configuration.md)** with allocated resources.
5. **[Set up core services](Setup_Guides/Server_Configuration)** (Active Directory, DNS, DHCP, File Server, etc.).
6. **Secure the network** with **pfSense [firewall](Setup_Guides/Firewall_Configuration.md) & [VPN](Setup_Guides/VPN_Configuration)**.
7. **Deploy cybersecurity tools** (SIEM, IDS/IPS, Pentesting tools): Wazuh, Suricata, etc.
8. **Simulate the Network** with [GNS3](Setup_Guides/GNS3.md)
9. **Simulate enterprise applications** (Web server, Database, Email, Docker apps).
10. **Perform security testing** with [Kali Linux](Security/Kali_Pentest) & [Metasploitable](Security/Metasploit).

[Back to Top](#top)

---

## Lab Infrastructure
| **VM Name** | **OS** | **Role** | **Purpose** |
|------------|--------|----------|-------------|
| **DC1** | Windows Server 2022 | Active Directory, DNS, DHCP | Centralized authentication & network services |
| **FS1** | Windows Server 2022 | File & Print Server | Shared file storage & network printers |
| **MAIL** | Windows Server 2022 / Ubuntu Server | Email Server | Internal email system |
| **WSUS** | Windows Server 2022 | Update Server | Manage Windows updates |
| **FIREWALL** | pfSense | Network Security | Firewall, VPN, & traffic filtering |
| **SIEM** | Ubuntu Server | Security Monitoring | Log analysis, threat detection (Wazuh) |
| **IDS/IPS** | Ubuntu Server | Intrusion Detection | Network security monitoring (Suricata) |
| **GNS3** | Ubuntu Server | Network Simulation | CCNA-level virtual network lab |
| **WEB1** | Ubuntu Server | Web Server | Hosts websites & applications |
| **DB1** | Ubuntu Server | Database Server | Manages SQL databases |
| **DOCKER** | Ubuntu Server | Containerized Apps | Run microservices & DevOps workloads |
| **KALI** | Kali Linux | Pentesting Workstation | Ethical hacking & security testing |
| **METASPLOIT** | Metasploitable | Vulnerable VM | Cybersecurity practice target |
| **BACKUP** | Ubuntu Server | Backup & Recovery | Disaster recovery & backup system |

[Back to Top](#top)

---

## 📜 Documentation
- **[Proxmox Installation & VM Setup](Setup_Guides/Proxmox_Install.md)**
- **[Server Configuration](Setup_Guides/Server_Configuration.md)**
- **[pfSense Firewall Setup](Setup_Guides/pfSense.md)**
- **[Network Simulation (GNS3)](Setup_Guides/GNS3.md)**
- **[Pentesting with Kali & Metasploitable](Security/Kali_Pentest.md)**
- **[Docker & Web Apps](Setup_Guides/Docker_Web.md)**

[Back to Top](#top)

---

## 🚀 Future Improvements
- Add **SIEM threat hunting scenarios**.
- Deploy **enterprise applications** (e.g., ERP, CRM, VoIP).
- Implement **high availability & failover** for critical services.
- 

[Back to Top](#top)

---

## Advanced Hands-On Activities
- Advanced activities will be listed here once everything has been set up.

[Back to Top](#top)

---

## Troubleshooting
- Please refer **[here](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/tree/main/Troubleshooting)** for a list of problems you might encounter and how to possibly solve them.
- Incident response section will be added once all the servers and services has been set up.

[Back to Top](#top)

---

## 🏆 Why This Project Matters
This home lab serves as a **hands-on learning platform** to strengthen skills in **IT, networking, and cybersecurity**. It enables one to experience setting up various IT infrastructures that provide real-world support to businesses. Additionally, it offers a safe environment to hone and practice Ethical Hacking skills legally, fostering continuous learning and professional growth.

[Back to Top](#top)

---


---
🔹 *This repository will be updated as the lab evolves.* Feel free to contribute ideas or improvements! Let's gooo!!!
