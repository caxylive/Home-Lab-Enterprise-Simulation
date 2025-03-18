<a name="top"></a>
[Back to Main](https://github.com/caxylive/Home-Lab-Enterprise-Simulation/blob/main/README.md)

---

# Proxmox Service Monitoring and Automated Recovery Guide

---

## Overview

This guide provides step-by-step instructions for ensuring the Proxmox web interface (`pveproxy`) remains active at all times by using a custom monitoring script. It avoids intrusive watchdog mechanisms that disrupt workflows and ensures minimal downtime, even after events like total shutdowns, low-battery shutdowns, or waking from sleep.

[Back to Top](#top)

---

## Steps

### 1. Create a Custom Monitoring Script

This script checks the status of the `pveproxy` service every 5 seconds and restarts it if needed.

#### 1. Create the script:
#### 2. Add the following content:
#### 3. Make the script executable:

[Back to Top](#top)

---

### 2. Automate Script Execution

To ensure the script starts at boot and runs continuously in the background:

#### 1. Edit crontab:
#### 2. Add the following line to run the script at system startup:
  * `@reboot` : Ensures the script runs automatically after the system boots.
  * `&` : Runs the script in the background, so it doesn't block other processes.

#### 3. Save and exit the crontab editor.

[Back to Top](#top)

---

### 3. Verify the Setup

#### 1. Reboot the server to confirm that the script starts automatically:
#### 2. After rebooting, check if the script is running:
#### 3. Manually stop the `pveproxy` service to test recovery:
#### 4. Wait 5 seconds and verify that the service restarts automatically:

[Back to Top](#top)

---

### 4. Key Benefits

* **Workflow-Friendly**: The script ensures minimal interruptions, as it only acts when `pveproxy` stops running.

* **Non-intrusive**: Unlike a traditional watchdog, this script does not proactively restart the service unnecessarily.

* **Lightweight**: The simple script runs in the background without straining system resources.

[Back to Top](#top)

---

### Notes

* This setup is particularly useful when remotely connecting to Proxmox through its web interface, as it keeps the `pveproxy` service running consistently.

* If adjustments to the 5-second interval are needed, simply modify the `sleep 5` line in the script.

* Future enhancements could include additional monitoring for other critical services if desired.
