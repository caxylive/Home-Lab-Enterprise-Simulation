# 🏠 Home Lab - Enterprise IT & Cybersecurity Simulation

## 📌 Overview
This project documents my journey in building a **home lab** that simulates a real-world (small-medium business) **enterprise IT environment**. It includes detailed instructions for hardware setup, software installations, network configurations, and hands-on cybersecurity practices. The goal is to gain **hands-on experience** with:
- **System Administration** (Windows Server, Active Directory, DNS, DHCP, File Sharing)
- **Networking** (pfSense Firewall, VPN, GNS3 Network Simulations)
- **Cybersecurity** (SIEM, IDS/IPS, Penetration Testing with Kali Linux & Metasploitable)
- **DevOps & Virtualization** (Proxmox, Docker, Web & Database Servers)

## Table of Contents
1. [Hardware](#hardware)
2. [Software Requirements](#software-requirements)
3. [Setup Process](#-setup-process)
4. [Lab Infrastructure](#lab-infrastructure)
5. [Documentation](#-documentation)
6. [Future Improvements](#-future-improvements)
7. [Advanced Hands-On Activities](#advanced-hands-on-activities)

## Hardware
- **Laptop**: LG Gram 16 with Intel Core i7-1260P, 16GB RAM, and two 1TB SSDs.
- **Mini PC**: [Beelink](https://www.lazada.com.ph/products/beelink-mini-pc-ser7ser6-max-ryzen-7-7840hs-7735hs-radeon-780m-ddr5-pcie40-ssd-quad-display-wifi6-bluetooth-52-desktop-computer-i4302917834-s24152074171.html?) (coming soon).

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

## 🔧 Setup Process
1. **Install Proxmox VE** on the host machine.
2. **Create and configure VMs** with allocated resources.
3. **Set up core services** (Active Directory, DNS, DHCP, File Server, etc.).
4. **Secure the network** with **pfSense firewall & VPN**.
5. **Deploy cybersecurity tools** (SIEM, IDS/IPS, Pentesting tools).
6. **Simulate enterprise applications** (Web server, Database, Email, Docker apps).
7. **Perform security testing** with Kali Linux & Metasploitable.

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

## 📜 Documentation
- **[Proxmox Installation & VM Setup](Setup_Guides/Proxmox_Install.md)**
- **[Windows Server Configuration](Setup_Guides/Windows_Server.md)**
- **[pfSense Firewall Setup](Setup_Guides/pfSense.md)**
- **[Network Simulation (GNS3)](Setup_Guides/GNS3.md)**
- **[Pentesting with Kali & Metasploitable](Security/Kali_Pentest.md)**
- **[Docker & Web Apps](Setup_Guides/Docker_Web.md)**

## 🚀 Future Improvements
- Add **SIEM threat hunting scenarios**.
- Deploy **enterprise applications** (e.g., ERP, CRM, VoIP).
- Implement **high availability & failover** for critical services.

## 🏆 Why This Project Matters
This home lab serves as a **hands-on learning platform** to strengthen my skills in **IT, networking, and cybersecurity**, preparing me for **certifications (Network+, Security+, CCNA)** and a **career transition into IT**.

---
🔹 *This repository will be updated as the lab evolves.* Feel free to contribute ideas or improvements!
